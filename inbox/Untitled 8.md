## 描述

custom http hook

回傳：

- isLoading

- error

- sendRequest -> 回傳給其他元件來發送請求

  

製作一個custom hook function

- 業務邏輯保持著通用且能夠讓其他元件使用，盡量不局限於特定項目，方式：
	- 定義設定物件，專門用作於業務邏輯使用
	- 定義額外(並不能成為通用的)函式物件於custom hook function呼叫
- 命名方式保持著通用


若在custom hook 中的useCallback deps 會是useHttp(options, applyData)中的options 和applyData。

  

且options和applyData會是物件，在這裡為了避免無限迴圈，得使用以下方法：

- options 由於為一般物件，所以使用useMemo或者不以options作為deps

- applyData 由於為函式物件，所以使用useCallback來解決

  

options 由於為一般物件，不作為deps的做法：由於options最終會用在sendRequest當參數來使用，不如成為該函式的參數，然後回傳至元件中，再讓元件自己去bind

  

結論為

1. 將options 和 applyData 分別使用useMemo和useCallback來解決

2. 試著將options和apply 不設定為custom hook 中的useCallback deps => 藉由減少deps而減少複雜度



### 試著將options和apply 不設定為custom hook 中的useCallback deps

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