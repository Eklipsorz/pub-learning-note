## 描述

```
const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn);
```

useReducer 會回傳兩個元素的陣列：
	- state 是目前狀態的snapshot
	- dispatchFn 是更新狀態的snapshot


dipatchFn 主要會派遣action至useReducer中的reducerFn中，其dipatchFn形式如下：
	- action 是定義著分派給reduceFn的任務是什麼
```
dipatchFn(action)
```

舉例：
```
 dispatch({ type: "COMPLETE", id: todo.id });
```

reducerFn 為 
- 依據action 來回傳狀態、更新狀態&觸發渲染週期，並於每一次渲染週期分配新狀態值給state，其引數為兩個，分別為prevState 和 action
- prevState 為 先前狀態，其狀態會是指React 層級所管理的，action 則是指dispatch所製造的action
- 只要一旦接收到由dispatch所製造的action 就自動執行：接收目前狀態的snapshot、處理並回傳新狀態、更新狀態、觸發渲染週期

```
(prevState, action) => {
	.....
}
```



 >(prevState, action) => newState
> A function that is triggered automatically once an action is dispatched (via dispatchFn()) – it receives the latest state snapshot and should return the new, updated state.


initialState ：定義初始狀態
> The initial state

initFn
> a function to set the initial state programmatically

主要是定義如何設定初始值


### dispatchFn

action ： it can be a string identifier ，具體定義由開發者定義

e.g., 'NEW_EMAIL_VALUE' or number or  {....}

  

常見是將action當成任務代號，並由reducer解析代號來產生對應的狀態。

  

命名方式會是由物件包含著，屬性會有type和payload

dispatchEmail({type: .....,value})


### reducerFn

useReducer 中的 reducerFn 定義會另外定義成named function 並放在component之外，這是為了確保reducerFn 並不會接收到component 裡頭的資料，因為沒必要去與component裡頭的資料進行互動以及保證只會用到全域或者reducer函式內所定義/接收到的資料

  

> All the data which will be required and used inside of the reducer function will be passed into this function when it's executed by React, automatically.


> now with the help of useReducer. And this allows us to group this emailState together and manage it in one place




> reducer 給定的function(state, action)

> state 會被保證一定是目前最新的狀態
>
> So therefore I'll use my last state snapshot, which i get here. And that this is guaranteed to be the absolute last state snapshot

> reducer 開發上會依據action給予的資訊來調整要回傳的狀態是什麼？




### reduce / reduction
> reduction refers to **the rewriting of an expression into a simpler form**.

重點：
- reduce 是將複雜的事物轉換成單一簡單的事物

### reducer 命名緣由
負責將複雜事物轉換成單一簡單事物的函式、儀器、機器，在這裡會是將多個狀態合併一個狀態來管理。

## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: