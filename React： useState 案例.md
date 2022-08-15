
## 描述



useState 使用方法：

1. 從React Library 來載入對應函式

`import { useState } from 'react';`

[[@reactReactUseStateHook]]
> We initialize our state by calling `useState` in our function component.
> `useState` accepts an initial state and returns two values:
> -   The current state.
> -   A function that updates the state.


```
const [title, setTitle] = useState(inialValue)
```
1. useState 會建立一個特殊變數來代表特定元件下的狀態，而狀態會是指某個時期下，對應元件的內容是什麼
2. 該特殊變數的初始值會是initialValue
3. useState 會回傳一組陣列：
	- 第一個元素是會是特殊變數的目前值或者目前狀態
	- 第二個元素則是專門更新該特殊變數狀態的函式 
4. 專門更新該特殊變數狀態的函式 會是負責做：
	- 更新特殊變數的目前狀態
	- 負責再次呼叫目前元件所對應的函式進行更新內容後的渲染

總結起來，在這裡會用title來接收目前狀態，使用setTitle來接收負責再次更新&渲染用的函式


#### 使用方式：專門更新該特殊變數狀態的函式
使用方式如下：直接丟修改內容當參數呼叫setTitle
```
setTitle(newTitle)
```

當事件發生時，可以調用以上函式來重新更新內容和渲染

#### 當事件發生時為何不直接更新title的值？

當事件發生時，直接以下面形式更新的話，不會觸發對應渲染，在這裡的title也只是接收目前狀態的內容，而非物件。
```
title = newTitle
```

為了解決以下內容所提到的問題
[[React：為何直接更改元件下的內容而得不到對應渲染畫面？這是因為內容有更新，但沒自動重新執行對應函式來重新渲染成內容更新後的元件樣貌]]

#### 更新：當使用專門更新該特殊變數狀態的函式
當執行專門更新該特殊變數狀態的函式時，會以最新狀態來渲染對應元件的內容但

```
function ExpenseItem(props) {
	const [title, setTitle] = useState(inialValue);
	
	const clickHandler = () => {
		setTitle('updated!!');
		console.log(title);
	};
	
	return (
		.....
	);
}
```
原則上title 本身就是存放目前狀態副本的變數，不是以物件參照來去更新對應內容，所以當執行setTitle來更新特殊變數的狀態值，本來就不會更動title這變數。

但由於setTitle會再次呼叫元件的對應函式來執行和獲取對應畫面，當然在這裡並不會重複建立特殊變數以及不會再次分配初始值給目前特殊變數，但會讓title、setTitle獲取到最新的狀態和對應狀態的更新函式
```
useState(inialValue);
```

## 複習


---
Status: 
Tags:
Links:
References:
[[@reactReactUseStateHook]]