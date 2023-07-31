## 描述

使用以下內容所提的策略來應用至負責增加任務的元件，讓它呼叫useHttp
[[React：custom hook function之開發策略可根據hook function是否加入引數而分為兩個開發策略-僅保持通用和邊保持通用邊盡可能減少hook內部的deps需求方向]]
### 增加任務的元件呼叫useHttp

```
import Section from '../UI/Section';
import TaskForm from './TaskForm';
import useHttp from '../../hooks/use-http';

const NewTask = (props) => {
  const { isLoading, error, sendRequest } = useHttp();

  const createTask = (taskText, data) => {
    const generatedId = data.name; // firebase-specific => "name" contains generated id
    const createdTask = { id: generatedId, text: taskText };

    props.onAddTask(createdTask);
  };

  const enterTaskHandler = async (taskText) => {
    sendRequest(
      {
        url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/tasks.json',
        method: 'POST',
        body: { text: taskText },
      },
      createTask.bind(null, taskText),
    );
  };

  return (
    <Section>
      <TaskForm onEnterTask={enterTaskHandler} loading={isLoading} />
      {error && <p>{error}</p>}
    </Section>
  );
};

export default NewTask;
```


#### bind 的妙用

原本createTask是擁有兩個引數的函式，並且當作useHttp所回傳的sendRequest作為呼叫使用

App.js
```
  const createTask = (taskText, data) => {
    const generatedId = data.name; // firebase-specific => "name" contains generated id
    const createdTask = { id: generatedId, text: taskText };

    props.onAddTask(createdTask);
  };
```

但由於use-http.js是使用一個參數，且是使用App.js的createTask所擁有的第二個引數，為了繼續讓use-http.js成為通用的hook，所以使用bind來將createTask改造成專門綁定taskText的createTask並傳入至use-http.js，就能以傳入data形式來執行
```
handler(data);
```

## 複習




---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：custom hook function之開發策略可根據hook function是否加入引數而分為兩個開發策略-僅保持通用和邊保持通用邊盡可能減少hook內部的deps需求方向]]
[[React：custom hook 在component使用就如同函式呼叫那樣使用，其搭載的hook和custom hook會註冊在該component上]]
[[React：定義 custom hook 以及注意事項]]
References: