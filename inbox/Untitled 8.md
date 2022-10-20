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

接著App.js


在這裡App

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
      url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/tasks.json',
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


試著將options和apply 不設定為custom hook 中的useCallback deps

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

const options = {
  url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/tasks.json',
};

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
    fetchTasks(options, fetchDataHandler);
  }, []);

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

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：custom hook 在component使用就如同函式呼叫那樣使用，其搭載的hook和custom hook會註冊在該component上]]
[[React：定義 custom hook 以及注意事項]]
References: