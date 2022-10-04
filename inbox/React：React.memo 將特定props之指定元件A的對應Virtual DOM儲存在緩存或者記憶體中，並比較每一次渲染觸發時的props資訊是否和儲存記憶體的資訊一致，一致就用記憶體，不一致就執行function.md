## 描述

[[@reactReactDingCengAPI]]
> React.memo 是一個 higher order component。

> 如果你的 function component 每次得到相同 prop 的時候都會 render 相同結果，你可以將其包在 React.memo 之中，透過快取 render 結果來在某些情況下加速。這表示 React 會跳過 render 這個 component，並直接重用上次的 render 結果。

> React.memo 只會確認 props 的改變。如果你的 function component 被 wrap 在 React.memo 內，實作中具有一個 useState、useReducer 或 useContext Hook，當 state 或 context 改變時，它仍然會持續 rerender。

> 這預設只會對 prop 進行 shallow compare 。如果你需要控制比較的方法，你可以提供一個自訂的比較 function 作為第二個參數。

```
function MyComponent(props) {
  /* render using props */
}
function areEqual(prevProps, nextProps) {
  /*
  return true if passing nextProps to render would return
  the same result as passing prevProps to render,
  otherwise return false
  */
}
export default React.memo(MyComponent, areEqual);
```


重點：
- React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中
	- 當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準
		- 預設特定規則會是 **目前傳遞至元件A的props 資訊是否與緩存儲存的props資訊一樣的**
		- 若達到的話，就直接回傳緩存或者記憶體中的元件A之對應Virtual DOM
		- 若沒達到的話，就直接執行指定元件A的渲染函式以此來得到對應元件的Virtual DOM，並且將對應元件的Virtual DOM和當時的props資料儲存起來好用來比對下一次。
- 語法會是
	- component 會是指的是要暫存的指定元件A，具體會以component function來表示
	- callback 則是定義是否要以緩存的Virtual DOM來使用的標準，其函式會回傳true或者false：
		- true，就通知React使用緩存的Virtual DOM來回傳，不執行對應元件的component function
		- false，就通知React直接執行對應元件的component function，不用緩存的Virtual DOM
	- 回傳值會是 會被記憶體儲存的component 結果 或者 執行對應元件的渲染後所獲得的component 結果，其結果為Virtual DOM
```
React.memo(component, callback)
```

### 實驗：定義是否使用緩存中Virtual DOM的callback

```
import React from 'react';
import Wrapper from './Wrapper';
const DemoOutput = (props) => {
  console.log('DemoOutput RUNNING');
  return <Wrapper>{props.show ? 'This is new!' : ''}</Wrapper>;
};

function trulyValue() {
  return true;
}

function falsyValue() {
  return false;
}

export default React.memo(DemoOutput);
```


```
export default React.memo(DemoOutput, trulyValue);
```
執行以上會得到
```
APP RUNNING
Button RUNNING
```


```
export default React.memo(DemoOutput, falsyValue);
```
執行以上會得到
```
APP RUNNING
DemoOutput RUNNING
Wrapper RUNNING
Button RUNNING
```

重點：
- 當callback回傳ture，那麼當React想要觸發DemoOutput的渲染函式，就不直接執行該渲染函式，改用位於緩存的Virtual DOM
- 當callback回傳false，那麼當React想要觸發DemoOutput的渲染函式，就直接執行該渲染函式，不用位於緩存的Virtual DOM

### 儲存在記憶體的Virtual DOM會是一開始的版本？

```
import React, { useState } from 'react';

import Button from './components/UI/Button/Button';
import DemoOutput from './components/Demo/DemoOutput';
import './App.css';

function App() {
  const [showParagraph, setShowParagraph] = useState(false);
  const [count, setCount] = useState(0);
  console.log('APP RUNNING');

  const toggleParagraphHandler = () => {
    console.log('count: origin: %', count, count % 5);
    setCount((count) => count + 1);
    setShowParagraph(Boolean(count % 5));
  };

  return (
    <div className='app'>
      <h1>Hi there!</h1>
      <DemoOutput show={showParagraph} />
      <Button onClick={toggleParagraphHandler}>Toggle Paragraph!</Button>
    </div>
  );
}

export default App;
```


```
APP RUNNING
DemoOutput.js:4 DemoOutput RUNNING
Wrapper.js:4 Wrapper RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 0 0
App.js:10 APP RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 1 1
App.js:10 APP RUNNING
DemoOutput.js:4 DemoOutput RUNNING
Wrapper.js:4 Wrapper RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 2 2
App.js:10 APP RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 3 3
App.js:10 APP RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 4 4
App.js:10 APP RUNNING
Button.js:6 Button RUNNING

App.js:13 count: origin: % 5 0
App.js:10 APP RUNNING
DemoOutput.js:4 DemoOutput RUNNING
Wrapper.js:4 Wrapper RUNNING
Button.js:6 Button RUNNING
```

- mounting階段由於記憶體沒對應元件的Virtual DOM，所以會觸發的component function 而產生對應的Virtual DOM和對應props存放在記憶體中，props.show = false
- 當按鈕發生點擊事件時，也就是觸發第一次的updating，那時會取得到的props會是false，所以就以記憶體為主
- 接著在點擊第二次點擊事件時，也就是觸發第二次的updating，那時會取得到的props會是true，所以會被判定不一樣而儲存那時的Virtual DOM和props值，props.show = true
- 接著在點擊第三次點擊事件時，也就是觸發第二次的updating，那時會取得到的props會是true，所底被判定與前一次相同而以記憶體為主
- 隨後依照這個規則來進行

總結：
- 第一次執行時 以及 與前次props值不一樣時 會執行對應component function來得到Virtual DOM並與props儲存在記憶體，好比對其標準是否滿足。

### 過去文獻參考
```
import React from 'react';
import Wrapper from './Wrapper';
const DemoOutput = (props) => {
  console.log('DemoOutput RUNNING');
  return <Wrapper>{props.show ? 'This is new!' : ''}</Wrapper>;
};

export default React.memo(DemoOutput);
```

It tells React that for this component which it get as a argument,
- React should look at the props this component gets and check the new value for all those props and compare it to the previous value those props got
- And only if the value of a prop changed, the component should be re-executed and re-evaluated.
- And if the parent component changed but the props values for that component here did not change, component execution will be skipped

  

React.memo(component)
- 當它正要被觸發渲染函式時，會檢查其props是否有變動，有變動才會執行對應渲染函式，否則就不執行



React.memo
- This is for functional components, allow us to optimize functional components
- For class-based components, this does not work.


tell React that is should only re-execute this DemoOutput component under certain circumstances：
- circumstances would be that props, which this component received, changed

### memorize 命名緣由
[[@wikidataMemorization2022]]
> Memorization is the process of committing something to memory.

重點：
- Memorization 是一個提交特定事物並永久儲存在記憶體的行為或者過程
- Memorize 則是提交特定事物並永久儲存在至記憶體

## 複習

#🧠 memorize 命名緣由 ->->-> `Memorize 則是提交特定事物並永久儲存在至記憶體`

#🧠 React.memo 是什麼？ ->->-> `如字面上的意思，React.memo 將特定props之指定元件A的對應Virtual DOM和對應props資訊儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function`

#🧠 React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準，請問標準達成會做什麼？->->-> ` 若達到的話，就直接回傳緩存或者記憶體中的元件A之對應Virtual DOM`

#🧠 React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準，請問標準沒達成會做什麼？ ->->-> `若沒達到的話，就直接執行指定元件A的渲染函式以此來得到對應元件的Virtual DOM，並且將對應元件的Virtual DOM和當時的props資料儲存起來好用來比對下一次。`


#🧠 React.memo 語法形式為何？ ->->-> `React.memo(component, callback)`

#🧠 React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準，請問標準可以自訂嗎？ ->->-> `可以`

#🧠 React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準，請問標準可允許自訂，但沒設定會是？ ->->-> `採取預設標準，標準為目前傳遞至元件A的props 資訊是否與緩存儲存的props資訊一樣的`

#🧠 React.memo(A, B) 中的 A 和 B分別為何？ ->->-> `A會是指的是要暫存的指定元件A，具體會以component function來表示，B為callback，其定義是否要以緩存的Virtual DOM來使用的標準，其函式會回傳true或者false`

#🧠 React.memo(A, B) 中的 A 和 B分別為何？B為callback，其定義是否要以緩存的Virtual DOM來使用的標準，其函式會回傳true或者false，那麼true和false會做什麼？ ->->-> `	- true，就通知React使用緩存的Virtual DOM來回傳，不執行對應元件的component function - false，就通知React直接執行對應元件的component function，不用緩存的Virtual DOM`

#🧠 React.memo(A, B) 回傳內容為何？ ->->-> `會被記憶體儲存的component 結果 或者 執行對應元件的渲染後所獲得的component 結果`


#🧠 React.memo(A, B) 回傳內容為會被記憶體儲存的component 結果 或者 執行對應元件的渲染後所獲得的component 結果，其結果會是 ->->-> `Virtual DOM`


#🧠 解釋一下React.memo 在這裡效果會是如何？從count=0至count=5會是如何印DemoOutput RUNNING和Button RUNNING？其中Button.js會固定印Button RUNNING ，而Wrapper.js 會固定印Wrapper RUNNING![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664910620/blog/react/memo/react-memo-app_b6ioum.png)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664910790/blog/react/memo/react-memo-DemoOuput_ws01ho.png)->->-> `- mounting階段由於記憶體沒對應元件的Virtual DOM，所以會觸發的component function 而產生對應的Virtual DOM和對應props存放在記憶體中，props.show = false - 當按鈕發生點擊事件時，也就是觸發第一次的updating，那時會取得到的props會是false，所以就以記憶體為主 - 接著在點擊第二次點擊事件時，也就是觸發第二次的updating，那時會取得到的props會是true，所以會被判定不一樣而儲存那時的Virtual DOM和props值，props.show = true - 接著在點擊第三次點擊事件時，也就是觸發第二次的updating，那時會取得到的props會是true，所底被判定與前一次相同而以記憶體為主 - 隨後依照這個規則來進行`

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：higher-order-component 是指專門以component function C 為參數作為處理並產出component function B為結果的 component function A]]
References:
[[@wikidataMemorization2022]]
[[@reactReactDingCengAPI]]