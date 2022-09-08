

## 描述
### 目標狀態內部分狀態是依賴著過去狀態

在這裏是會有三個輸入欄位分別是標題、價格、日期，標題輸入欄位的改變事件是由titleChangeHandler負責，價格輸入欄位的改變事件是由amountChangeHandler負責，最後日期輸入欄位的改變事件是由dateChangeHandler負責。

在這裏當title輸入欄位發生改變時，會將新title和舊有的欄位值搭配在一起來更新狀態。



```
function ExpenseForm(props) {

	const [userInput, setUserInput] = useState({
		enteredTitle: '',
		enteredAmount: '',
		enteredDate: ''
	})
  
	const titleChangeHandler = (event) => {
		const enteredTitle = event.target.value
		setUserInput({...userInput, enteredTitle})
	}

	const amountChangeHandler = (event) => {
		const enteredAmount = event.target.value
		setUserInput({...userInput, enteredAmount})
	}

	const dateChangeHandler = (event) => {
		const enteredDate = event.target.value
		setUserInput({...userInput, enteredDate})
	}
	.
	.
	.
	.
}
```



在這裡會是拿著userInput中來取得舊有的欄位值，在這裏userInput會是每一次渲染剛開始會拿到的資料，而在執行setUserInput時並不會立即改變狀態&渲染並刷新userInput值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**，這使得從要求更改狀態至完成狀態改變&渲染之間是有時間差


### 若面對大量更改狀態要求的情況下
主要是不一致的問題：若面對大量更改狀態要求的情況下，從要求更改狀態至完成狀態改變&渲染之間的時間差會逐漸加重，甚至沒辦法透過渲染而得到最新值，使得每一次渲染剛開始會拿到的資料會是最舊的資料


#### 解法

在setState中添加callback，就能將setState目前所要更改的狀態填入至callback當參數並且輸出成新的目標狀態來當更新狀態&渲染的目標
```
function setState(callback) {
	const newState = callback(currentState)
	// update with newState.....

}
```

這樣能使setState在每一次要求更新狀態時，都能以上一個setState所要求的狀態為基礎來要求更改額外的狀態

## 複習

#🧠 React：請問每當執行setState會立即更改狀態&渲染嗎？還是有時間差？為什麼？ ->->-> `在執行setState時並不會立即改變狀態&渲染並刷新state值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**，這使得從要求更改狀態至完成狀態改變&渲染之間是有時間差`
<!--SR:!2022-09-27,20,250-->

#🧠 React：請問每次執行setState時，從要求更改狀態至完成狀態改變&渲染之間是有時間差，具體是為什麼？ ->->->`在執行setState時並不會立即改變狀態&渲染並刷新state值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**`
<!--SR:!2022-09-09,10,250-->

#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行setState所得到的時間差會變成如何 ->->-> `時間差會使要求逐漸累績起來，進而加重時間差`
<!--SR:!2022-10-04,26,250-->


#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行State所得到的時間差會被加重，那麼對於this.setState({...state1, a})且state1是源自於useState所回傳的值來說會有什麼潛在問題? 為什麼(以依賴、渲染來說明)->->-> `主要是不一致的問題，由於狀態都是依賴著state1來更改，state1是必須透過渲染才能拿到最新狀態，然而在時間加重到無法透過渲染更新狀態，目前state1很有可能會是較舊，若中間有部分資料要更新的話`
<!--SR:!2022-09-09,10,250-->

#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行State所得到的時間差會被加重，那麼對於this.setState({...state1, a})且state1是源自於useState所回傳的值來說會有不一致的問題，那麼解法會是什麼？ ->->-> `使用callback當作setState參數，並用callback來取得較新的狀態state1`
<!--SR:!2022-09-09,10,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
References: