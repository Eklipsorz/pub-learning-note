## 描述

###  若要製作一個custom hook function來給予其他component使用

hook function內部
- 業務邏輯保持著通用且能夠讓其他元件使用，盡量不局限於特定項目，方式：
	- 可以定義設定物件，專門根據需求方的不同需求來衍生不同業務邏輯使用
	- 可以定義函式物件，專門根據需求方的不同需求之處理放置hook內部執行
- 命名方式保持著通用
- 開發策略可以根據hook function是否加入引數而分為兩個開發策略：
	- 僅保持通用：在這裡會選擇加入引數，但有可能會增加內部的hook對於deps的需求數
	- 邊保持通用邊盡可能減少hook內部的deps需求方向：在這裡會選擇不加入引數，想藉由減少deps而減少複雜度

### 案例：僅保持通用

由於是選擇加入引數來進行開發，在這裡的useHttp會以下方作為引數：
- options：設定連線和請求
- handler：負責處理資料和渲染

來回傳isLoading、error、fetchDataHandler 這三個內容至App元件來使用。

接著App.js的useEffect 使用著fetchDataHandler來呼叫並設定其為deps，為了確保不會因為fetchTasks是物件而產生出無限循環問題，而特定在use-http.js 內部設定useCallback設定在要回傳的fetchTasks


此時useCallback的deps設定為\[\]就解決，但實際上還可以添加以下，因為這兩者本身就是元件內的變數和物件，會是能夠代表潛在互動的資訊
```
- options：設定連線和請求
- handler：負責處理資料和渲染
```

若添加至deps的話，就代表把無限循環的問題丟給App.js中的options和handler，為了能夠避免，得在App.js分別作以下措施才能夠避免：
	- options ：設定useMemo 來儲存，其中deps為\[\]
	- handler：設定useCallback 來儲存，其中deps為\[\]
App.js
```
import React, { useEffect, useState, useMemo, useCallback } from 'react';

import Tasks from './components/Tasks/Tasks';
import NewTask from './components/NewTask/NewTask';
import useHttp from './hooks/use-http';

function App() {
  const [tasks, setTasks] = useState([]);

  const options = useMemo(
    () => ({
      url: 'xxxx/tasks.json',
    }),
    [],
  );

  const fetchDataHandler = useCallback((data) => {
    const loadedTasks = [];

    for (const taskKey in data) {
      loadedTasks.push({ id: taskKey, text: data[taskKey].text });
    }

    setTasks(loadedTasks);
  }, []);

  const {
    isLoading,
    error,
    sendRequest: fetchTasks,
  } = useHttp(options, fetchDataHandler);

  useEffect(() => {
    fetchTasks();
  }, [fetchTasks]);

  const taskAddHandler = (task) => {
    setTasks((prevTasks) => prevTasks.concat(task));
  };

  return (
    <React.Fragment>
      <NewTask onAddTask={taskAddHandler} />
      <Tasks
        items={tasks}
        loading={isLoading}
        error={error}
        onFetch={fetchTasks}
      />
    </React.Fragment>
  );
}

export default App;
```

use-http.js
```
import { useState, useCallback } from 'react';

const useHttp = (options, handler) => {
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const sendRequest = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch(options.url, {
        method: options.method ? options.method : 'GET',
        headers: options.headers ? options.headers : {},
        body: options.body ? JSON.stringify(options.body) : null,
      });

      if (!response.ok) {
        throw new Error('Request failed!');
      }

      const data = await response.json();

      handler(data);
    } catch (err) {
      setError(err.message || 'Something went wrong!');
    }
    setIsLoading(false);
  }, [options, handler]);

  return { isLoading, error, sendRequest };
};

export default useHttp;
```



### 案例：邊保持通用邊盡可能減少hook內部的deps需求方向


在這裡採取的策略會是不添加參數至useHttp，試著減少hook內部對於deps的需求，首先先將use-http.js中的options、handler放到 sendRequest 指定的函式物件上作為其引數，好讓設定options、handler的權利丟還給App.js來做，這樣就免去在useHttp設定deps。


最後在App.js 那邊透過useHttp所獲得的fetchTasks來在useEffect那呼叫，同時以fetchTask作為其deps，而它的呼叫引數則是在useEffect內部定義並使用，而這樣會因為useEffect 內部定義的變數/物件無法代表著元件上互動而不用添加至deps，因為能決定執行effect終究還是useEffect以外的內容且是代表元件互動的資訊

```
  useEffect(() => {
    function fetchDataHandler(data) {
      const loadedTasks = [];

      for (const taskKey in data) {
        loadedTasks.push({ id: taskKey, text: data[taskKey].text });
      }

      setTasks(loadedTasks);
    }

    const options = {
      url: 'xxxx/tasks.json',
    };

    fetchTasks(options, fetchDataHandler);
  }, [fetchTasks]);
```


use-http.js
```
import { useState, useCallback } from 'react';

const useHttp = () => {
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const sendRequest = useCallback(async (options, handler) => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch(options.url, {
        method: options.method ? options.method : 'GET',
        headers: options.headers ? options.headers : {},
        body: options.body ? JSON.stringify(options.body) : null,
      });

      if (!response.ok) {
        throw new Error('Request failed!');
      }

      const data = await response.json();

      handler(data);
    } catch (err) {
      setError(err.message || 'Something went wrong!');
    }
    setIsLoading(false);
  }, []);

  return { isLoading, error, sendRequest };
};

export default useHttp;
```


app.js
```
import React, { useEffect, useState } from 'react';

import Tasks from './components/Tasks/Tasks';
import NewTask from './components/NewTask/NewTask';
import useHttp from './hooks/use-http';

function App() {
  const [tasks, setTasks] = useState([]);
  const { isLoading, error, sendRequest: fetchTasks } = useHttp();

  useEffect(() => {
    function fetchDataHandler(data) {
      const loadedTasks = [];

      for (const taskKey in data) {
        loadedTasks.push({ id: taskKey, text: data[taskKey].text });
      }

      setTasks(loadedTasks);
    }

    const options = {
      url: 'xxxx/tasks.json',
    };

    fetchTasks(options, fetchDataHandler);
  }, [fetchTasks]);

  const taskAddHandler = (task) => {
    setTasks((prevTasks) => prevTasks.concat(task));
  };

  return (
    <React.Fragment>
      <NewTask onAddTask={taskAddHandler} />
      <Tasks
        items={tasks}
        loading={isLoading}
        error={error}
        onFetch={fetchTasks}
      />
    </React.Fragment>
  );
}

export default App;
```


## 複習

#💻 請至/react-builder/question-review/custom-hook-project-adv領取題目，並切換至hook-wiht-parameter分支，請製作一個hook能夠頂替App.js發送請求的功能，請務必讓hook能夠插入引數 ->->-> `/react-builder/custom-hook-project-adv下 切換至without-deps-decrement分支即可看到答案`
<!--SR:!2022-11-02,10,250-->

#💻 請至/react-builder/question-review/custom-hook-project-adv領取題目，並切換至hook-wihtout-parameter分支，請製作一個hook能夠頂替App.js和/src/components/NewTask/NewTask.js發送請求的功能，請不要讓hook能夠插入任何引數 ->->-> `https://github.com/academind/react-complete-guide-code/blob/15-building-custom-react-hooks/code/06-adjusting-the-custom-hook/src/hooks/use-http.js`
<!--SR:!2022-11-30,28,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：custom hook 在component使用就如同函式呼叫那樣使用，其搭載的hook和custom hook會註冊在該component上]]
[[React：定義 custom hook 以及注意事項]]
References: