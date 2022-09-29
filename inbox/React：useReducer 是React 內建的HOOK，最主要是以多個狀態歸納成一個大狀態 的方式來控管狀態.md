## 描述


### useReducer 介紹
useReducer：
1. React 內建的HOOK
2. 用作於狀態管理(與useState相似，但比較多功能來處理較為複雜狀態)


> sometimes, you have more complex state - for example if it got multiple states, multiple ways of changing it or dependencies to other states


> multiple states that kind of belong together, that are managing the same thing, just different aspects of it


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663521208/blog/react/state/useReducer/useReducer-relationship_iid2qe.png)

### useReducer 語法介紹


```
const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn);
```

重點：
- useReducer 會註冊一個hook 在目前元件上，並且主要以 **多個狀態歸納成一個大狀態** 的方式來控管狀態。
- useReducer 會回傳兩個元素的陣列：
	- state 是目前狀態的snapshot，實際上是每一次渲染週期內來獲取當前狀態值來儲存，並非真是負責儲存每次狀態的變數
	- dispatchFn 是派送特定行動函式，其行動會是指定狀態要如何更新
- useReducer 載入方式
```
import { useReducer } from 'react';
```



### dispatchFn


 dipatchFn 主要會派遣action至useReducer中的reducerFn中，並觸發reducerFn來處理狀態、渲染， 其dipatchFn形式如下：
	- action 是定義著分派給reduceFn的任務是什麼
```
dipatchFn(action)
```

舉例：
```
 dispatch({ type: "COMPLETE", id: todo.id });
```



#### action 形式
[[@dmitripavlutinEasyGuideReact2021]]
> An _action object_ is an object that describes how to update the state.
> Typically, the action object would have a property `type` — a string describing what kind of state update the reducer must do.


> action ： it can be a string identifier 
> e.g., 'NEW_EMAIL_VALUE' or number or  {....}

重點：
- action 本身主要是定義如何更新狀態
- action 能填入的值可以是：
	- 字串，如'NEW_EMAIL_VALUE'
	- 數字
	- 物件
- 常見是使用物件，屬性會有type和payload：
	- type 是描述哪一種狀態更新
	- payload 則是狀態更新的目標狀態
```
dispatch(action)
dispatch('NEW_EMAIL_VALUE')
dispatch(1)
dispatch({type: ....., payload:...})
```



### reducerFn
 >(prevState, action) => newState
> A function that is triggered automatically once an action is dispatched (via dispatchFn()) – it receives the latest state snapshot and should return the new, updated state.



reducerFn 為 一個函式，具體會有兩個引數分別為prevState和action，主要用途為依據action指示的狀態更新請求內容來回傳新狀態、更新狀態、觸發渲染週期。
- prevState 為最近最新狀態的snapshot，其狀態會是指React 層級所管理的，action 則是reducer接收到的action，其action會由dispatchFn所產生
- 只要一旦接收到由dispatch所製造的action 就自動執行
- 形式會是如下：
	- new-state 會是新狀態
```
(prevState, action) => {
	return new-state
}
```



#### (prevState, action) 函式常見形式

```
function reducer(state, action) {
  let newState;
  switch (action.type) {
    case 'increase':
      newState = { counter: state.counter + 1 };
      break;
    case 'descrease':
      newState = { counter: state.counter - 1 };
      break;
    default:
      throw new Error();
  }
  return newState;
}
```

#### reducerFn 語法使用方式

1. useReducer 中的 reducerFn 定義會另外定義成named function 並放在component之外
2. 目的：為了確保
	- 不會因為渲染週期的觸發而再次定義一次
	- reducerFn 並不會接收到component 裡頭的資料，因為沒必要去與component裡頭的資料進行互動
	- 會用到全域或者reducer函式內所定義/接收到的資料

3. 形式：

```
const reducerFn = (prevState, action) => {
	//.....
	return new-state
}

function Component(props) {
	const [state, dispatch] = useReducer(reducerFn)
	//.....
}

export default Componet
```
  

> All the data which will be required and used inside of the reducer function will be passed into this function when it's executed by React, automatically.


> now with the help of useReducer. And this allows us to group this emailState together and manage it in one place

#### reducerFn 的 preState 是最新的？


> So therefore I'll use my last state snapshot, which i get here. And that this is guaranteed to be the absolute last state snapshot
 
 
同一個 useReducer 控管的所有state 被保證一定是目前最新的狀態，這是因為：
1. 目前狀態都會被React 儲存管理。
2. 狀態更新都是在dispatch 所發送的action 或者 由React內部提供。
3. 狀態都歸納成同一個狀態，不會有依賴舊有狀態的問題。


#### reducerFn 觸發的狀態渲染會有auto-batching

設定email輸入欄位的change事件處理會執行8次dispatch來向reducer提出8次更新狀態、渲染的請求，但結果最後執行一次狀態更新和渲染，並沒有8次的更新狀態、渲染

```
const reducer = (prevState, action) => {
  console.log('hi reducer');
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { value: action.value, isValid: action.value.includes('@') };
    case 'INPUT_BLUR':
      return { value: prevState.value, isValid: prevState.isValid };
    default:
      return { value: '', isValid: null };
  }
};

const Login = (props) => {
  const [emailState, emailDispatch] = useReducer(reducer, {
    value: '',
    isValid: null,
  });
  console.log('hi login component');
  /*
  
	  do something
	  
  */
  const emailChangeHandler = (event) => {
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '2' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '3' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    setFormIsValid(
      .........
    );
  };

	
}
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663439448/blog/react/state/useReducer/useReducer-auto-batching-experiment_k9ijrv.png)


### initialState
initialState ：定義初始狀態
> The initial state

### initFn
initFn：主要是定義如何設定初始值
> a function to set the initial state programmatically


### 用語緣由

#### dispatch 命名緣由

> the act of sending someone or something somewhere

重點：
- 將特定物件傳送至特定位置的行為

#### reduce / reduction 命名緣由
> reduction refers to **the rewriting of an expression into a simpler form**.

重點：
- reduce 是將複雜的事物轉換成單一簡單的事物

#### reducer 命名緣由
負責將複雜事物轉換成單一簡單事物的函式、儀器、機器，在這裡會是將多個狀態合併一個狀態來管理。

#### action 命名緣由
> the process of doing something, especially when dealing with a problem or difficulty

> something that you do


重點：
- 當要解決特定問題或者困難時所要做的行為

## 複習

#🧠 useReducer 是什麼？用做什麼 ->->-> `1. React 內建的HOOK 2. 用作於狀態管理(與useState相似，但比較多功能來處理較為複雜狀態)`
<!--SR:!2022-10-12,15,249-->


#🧠 dispatch 命名緣由 ->->-> `將特定物件傳送至特定位置的行為`
<!--SR:!2022-10-02,10,250-->

#🧠 reduce / reduction 命名緣由 ->->-> `reduce 是將複雜的事物轉換成單一簡單的事物`
<!--SR:!2022-10-02,10,250-->

#🧠 reducer 命名緣由 ->->-> `負責將複雜事物轉換成單一簡單事物的函式、儀器、機器`
<!--SR:!2022-10-16,17,250-->


#🧠 reducer 在React世界中是指什麼？ ->->-> `在這裡會是將多個狀態合併一個狀態來管理。`
<!--SR:!2022-10-02,10,250-->

#🧠 action 命名緣由？（請針對問題和困難來說) ->->-> `當要解決特定問題或者困難時所要做的行為`
<!--SR:!2022-10-02,10,250-->

#🧠 useReducer 語法形式是什麼？回傳什麼？ ->->-> `const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn); 回傳會是兩個元素的陣列`
<!--SR:!2022-10-02,10,250-->

#🧠 userReducer 在元件上做了什麼？用途是什麼？ ->->-> `useReducer 會註冊一個hook 在目前元件上，並且主要以 **多個狀態歸納成一個大狀態** 的方式來控管狀態。`
<!--SR:!2022-10-11,14,230-->


#🧠 React：const \[state, dispatchFn\] = useReducer(reducerFn, initialState, initFn); 中的state、dispatchFn 是什麼？請先簡答->->-> `state 會是取得目前狀態值的變數，dispatchFn 是派送特定行動函式，其行動會是指定狀態要如何更新`
<!--SR:!2022-10-01,9,250-->


#🧠 React： useReducer 中的 dispatchFn 會發送action至reducerFn，請問會如何發送->->-> `將action當dipatchFn的引數來呼叫dipatchFn(action)`
<!--SR:!2022-10-02,10,250-->

#🧠 React： 在useReducer 中的dipatchFn(action)，action會是什麼？->->-> ` 本身主要是定義如何更新狀態`
<!--SR:!2022-09-30,8,250-->

#🧠 React： 在useReducer 中的dipatchFn(action)，action能填入什麼？->->-> `	- 字串，如'NEW_EMAIL_VALUE' - 數字 - 物件`
<!--SR:!2022-10-02,10,250-->

#🧠 React： 在useReducer 中的dipatchFn(action)，action最常用的形式是物件，請問如何用物件來表示action->->-> `屬性會有type和payload：	- type 是描述哪一種狀態更新 - payload 則是狀態更新的目標狀態`
<!--SR:!2022-10-02,10,250-->

#🧠 React：用程式碼來調用useReducer中的dispatch派送type為increase，value為123的action->->-> `dispatch({type: 'increase', value: 123})`
<!--SR:!2022-10-02,10,250-->


#🧠 useReducer 載入方式 ->->-> `import { useReducer } from 'react';`
<!--SR:!2022-09-30,8,250-->


#🧠 React：const \[state, dispatchFn\] = useReducer(reducerFn, initialState, initFn); 中的initialState, initFn 是什麼？用途是什麼？ 請先簡答 ->->-> `定義初始狀態、主要是定義如何設定初始值`
<!--SR:!2022-10-01,9,250-->

#🧠 React：const \[state, dispatchFn\] = useReducer(reducerFn, initialState, initFn); 中的reducerFn 是什麼？用途是什麼？請先簡答 ->->-> `reducerFn 為 一個函式，具體會有兩個引數分別為prevState和action。用途為依據action指示的狀態更新請求內容來回傳新狀態、更新狀態、觸發渲染週期`
<!--SR:!2022-10-02,10,250-->


#🧠 React：reducerFn(prevState, action) 中的 prevState和action是什麼引數 ->->-> `prevState 為最近最新狀態的snapshot，其狀態會是指React 層級所管理的，action 則是reducer接收到的action，其action會由dispatchFn所產生`
<!--SR:!2022-10-12,15,249-->

#🧠 React：reducerFn(prevState, action) 主要回傳什麼？ ->->-> `新狀態`
<!--SR:!2022-10-02,10,250-->


#🧠 React：reducerFn(prevState, action)如何被觸發執行？ ->->-> `只要一旦接收到由dispatch所製造的action 就自動執行`
<!--SR:!2022-10-02,10,250-->

#🧠 React：reducerFn(prevState, action)被觸發執行後，會產生出什麼效果？ ->->-> `回傳新狀態、更新狀態、觸發渲染週期`
<!--SR:!2022-10-02,10,250-->

#🧠 React：假設n個連續dispatch指令來派送action至reducer，reducerFn(prevState, action)如何被觸發執行？ ->->-> `這n個連續dispatch指令會分別被處理`
<!--SR:!2022-10-01,9,250-->

#🧠 React：假設n個連續dispatch指令來派送action至reducer，這些reducerFn(prevState, action)被觸發執行後，會產生出什麼效果？ ->->-> `會以auto-batching的方式，將狀態試著合併，最後再以最後合併結果來更新狀態、觸發渲染週期`
<!--SR:!2022-10-07,11,230-->


#🧠 React：假設n個連續dispatch指令來派送action至reducer，這些reducerFn(prevState, action)被觸發執行後，會執行n次的狀態更新＋觸發渲染週期嗎？ ->->-> `並不會，而是會以auto-batching來執行`
<!--SR:!2022-09-30,8,250-->

#🧠 React：reducerFn主要會是什麼樣子的函式，其函式內容為何？用程式碼表示一下 ->->-> `(prevState, action) => { return new-state }`
<!--SR:!2022-10-17,18,250-->

#🧠 React：reducerFn(prevState, action)的preState 會是最近最新的狀態？為什麼？ ->->-> `同一個 useReducer 控管的所有state 被保證一定是目前最新的狀態，原因為：1. 目前狀態都會被React 儲存管理。 2. 狀態更新都是在dispatch 所發送的action 或者 由React內部提供。 3. 狀態都歸納成同一個狀態，不會有依賴舊有狀態的問題。`
<!--SR:!2022-10-02,10,250-->

#🧠 React：reducerFn定義上通常會在哪裡進行？ 為什麼？->->-> `useReducer 中的 reducerFn 定義會另外定義成named function 並放在component之外。 原因是：- 增加為了確保不被重複定義	- reducerFn 並不會接收到component 裡頭的資料，因為沒必要去與component裡頭的資料進行互動 - 會用到全域或者reducer函式內所定義/接收到的資料`
<!--SR:!2022-10-01,9,250-->



#🧠 React：reducerFn定義上通常會如何開發？考慮它會在哪以及誰會去用useReducer，用程式碼表示 ->->-> `const reducerFn = (prevState, action) => { //..... return new-state} function Component(props) { const [state, dispatch] = useReducer(reducerFn) //..... } export default Componet`
<!--SR:!2022-10-18,19,250-->

#🧠 React：假設派遣過來的action會是type為increase或者descrease，並且預期當reducer接收到increase就替狀態上的counter進行遞增以及當reducer接收到descrease就替狀態上的counter進行遞減，其餘則是發出錯誤，請問如何用程式碼表示 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663519501/blog/react/state/useReducer/useReducer-usage1_q8tnw6.png)`
<!--SR:!2022-10-01,9,250-->



#🧠 React：請畫圖來表示Component中的EventHandler、Dispatch、Reducer、State、render來表示useReduer 使用起來的關係圖 ->->-> `![](https://dmitripavlutin.com/5c33affee33e7c40e73028fb48a8367b/diagram.svg)`
<!--SR:!2022-10-02,10,250-->

#🧠 React：請問useReducer的狀態更新支不支援auto-batching ->->-> `支援`
<!--SR:!2022-10-01,9,250-->

#🧠 React：請問useReducer的派送action和處理action支不支援auto-batching ->->-> `都不支援`
<!--SR:!2022-10-16,17,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References:
[[@dmitripavlutinEasyGuideReact2021]]