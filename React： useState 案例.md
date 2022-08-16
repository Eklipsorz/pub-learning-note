
## 描述


### useState 放置位置
[[React： useState 案例]]
useState


useState 使用方法：

1. 從React Library 來載入對應函式

`import { useState } from 'react';`

[[@reactReactUseStateHook]]
> We initialize our state by calling `useState` in our function component.
> `useState` accepts an initial state and returns two values:
> -   The current state.
> -   A function that updates the state.


### useState 作用

useState 用途：
1. 負責生成能儲存狀態的特殊變數、該特殊變數的更新用函式並註冊目前它所在的元件實例：讓建立的元件實例擁有狀態
2. 管理/維護生成後的特殊變數、該特殊變數的更新用函式：讓每個已註冊好的元件實例都還能擁有自己的狀態

有效管理每個元件下的狀態，且不會落入以下問題
>多個相同元件的事件綁定處理：
> - 當一個元件發生事件，全部元件就引發對應事件處理

#### 狀態
狀態本身會是特定時間點下，某個事物下的內容，在這裡內容會是字串、物件、數字。

#### 舉例

e.g.,  在這裡有四個ExpenseItem，每一個會呼叫元件對應函式來渲染並各自生成特定特殊變數來註冊在目前所建立的元件實例，換言之會有四個特殊變數各自綁定第一項ExpenseItem、第二項ExpenseItem、....、第四項ExpenseItem，特殊變數會以狀態值來控制著每一項的內容。

```
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
```

### 首次使用useState
1.  useState 會以目前初始值(initialValue)來作為目前狀態來儲存的特殊變數A、該特殊變數A的更新用函式
2. 將特殊變數、更新用函式註冊給目前它所在的元件實例，換言之，N個擁有useState呼叫的實例都各有一組獨立特別變數A、更新用函式
3. 以陣列形式來回傳特殊變數A的目前狀態、更新用函式，形式會是如下：
	- 第一個元素是會是特殊變數A的目前值或者目前狀態
	- 第二個元素則是專門更新該特殊變數A狀態的函式 
	```
	const [status, setStatus] = useState(initialValue)
	```
	
注意事項：
- 設定const 在status、setStatus 是為了一開始分配後不被其他程式修改
- status單方面修改也並不會觸發渲染
```
status = xxxx
```

### setStatus 作用
專門更新該特殊變數A狀態的函式setStatus 會是負責做：
- 產生一個非同步更新任務來排程：該任務專門從React管理的特殊變數A的角度，來更新特殊變數A所存下的內容
- 以目前最新內容來執行目前元件所對應的函式來渲染成 **內容更新後的畫面**


#### 使用方式：專門更新該特殊變數狀態的函式
使用方式如下：直接丟修改內容當參數呼叫setStatus
```
setStatus(newContent)
```

當事件發生時，可以調用以上函式來重新更新 **對應元件實例下的內容和渲染**

#### 當事件發生時為何不直接更新title的值？

```
const [status, setStatus] = useState(initialValue)
```

當事件發生時，直接以下面形式更新的話，不會觸發對應渲染，在這裡的status也只是以變數形式接收目前狀態的副本，而非物件。
```
status = newStatus
```



### 首次使用後的useState
1. useState 會繼續使用以首次生成的特殊變數來儲存最新狀態
2. 以陣列形式來回傳特殊變數的目前狀態、更新用函式，形式會是如下
```
const [status, setStatus] = useState(inialValue)
```

注意事項為
- 並不會重新生成特殊變數來儲存初始值
- 不會拿現成的特殊變數來更新成初始值


#### 更新：當使用專門更新該特殊變數狀態的函式
當執行專門更新該特殊變數狀態的函式時，會以最新狀態來回傳最新狀態、對應特殊變數的更新

```
function ExpenseItem(props) {
	const [status, setStatus] = useState(inialValue);
	
	const clickHandler = () => {
		setStatus('updated!!');
		console.log(status);
	};
	
	return (
		.....
	);
}
```
但原則上status本身就是存放目前狀態副本的變數，不是以物件參照來去更新對應內容，所以當執行setStatus來更新特殊變數的狀態值，本來就不會更動status這變數。




但由於setStatus會再次呼叫元件的對應函式來執行和獲取對應畫面，當然在這裡並不會重複建立特殊變數以及不會再次分配初始值給目前特殊變數，但會讓status、setStatus獲取到最新的狀態和對應狀態的更新函式
```
useState(inialValue);
```



## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：hook]]
References:
[[@reactReactUseStateHook]]