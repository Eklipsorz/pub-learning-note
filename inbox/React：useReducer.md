## 描述


### useReducer 介紹
useReducer：
1. React 內建的HOOK
2. 用作於狀態管理(與useState相似，但比較多功能來處理較為複雜狀態)


> sometimes, you have more complex state - for example if it got multiple states, multiple ways of changing it or dependencies to other states


> multiple states that kind of belong together, that are managing the same thing, just different aspects of it


![](https://dmitripavlutin.com/5c33affee33e7c40e73028fb48a8367b/diagram.svg)

### useReducer 語法介紹


```
const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn);
```

重點：
- useReducer 會註冊一個hook 在目前元件上，並且主要以 **多個狀態歸納成一個大狀態** 的方式來控管狀態。
- useReducer 會回傳兩個元素的陣列：
	- state 是目前狀態的snapshot，實際上是每一次渲染週期內來獲取當前狀態值來儲存，並非真是負責儲存每次狀態的變數
	- dispatchFn 是更新狀態的snapshot
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
- prevState 為 先前狀態，其狀態會是指React 層級所管理的，action 則是指dispatch所製造的action
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
	- reducerFn 並不會接收到component 裡頭的資料，因為沒必要去與component裡頭的資料進行互動
	- 保證只會用到全域或者reducer函式內所定義/接收到的資料

3. 形式：

```
const reducerFn = (prevState, action) => {
	//.....
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
1. 目前狀態都會被React儲存。
2. 狀態更新都是在dispatch 所發送的action 或者 由React內部提供。
3. 狀態都歸納成同一個狀態，不會有依賴舊有狀態的問題。


#### reducerFn 觸發的狀態渲染會有auto-batching
對

```

```

### initialState
initialState ：定義初始狀態
> The initial state

### initFn
initFn：主要是定義如何設定初始值
> a function to set the initial state programmatically


### dispatch 命名緣由

> the act of sending someone or something somewhere

重點：
- 將特定物件傳送至特定位置的行為

### reduce / reduction 命名緣由
> reduction refers to **the rewriting of an expression into a simpler form**.

重點：
- reduce 是將複雜的事物轉換成單一簡單的事物

### reducer 命名緣由
負責將複雜事物轉換成單一簡單事物的函式、儀器、機器，在這裡會是將多個狀態合併一個狀態來管理。

### action 命名緣由
> the process of doing something, especially when dealing with a problem or difficulty

> something that you do


重點：
- 當要解決特定問題或者困難時所要做的行為

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References:
[[@dmitripavlutinEasyGuideReact2021]]