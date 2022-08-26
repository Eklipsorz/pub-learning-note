

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



在這裡會是拿著userInput中來取得舊有的欄位值，在這裏userInput會是每一次渲染剛開始會拿到的資料，


而在執行setUserInput時並不會立即改變狀態&渲染並刷新userInput值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**，這使得從要求更改狀態至完成狀態改變&渲染之間是有時間差


### 若面對大量要求更改狀態的情況下
若面對大量要求更改狀態的情況下，從要求更改狀態至完成狀態改變&渲染之間是有時間差會逐漸加重，甚至沒辦法透過渲染而得到最新值，使得每一次渲染剛開始會拿到的資料會是最舊的資料




## 複習


---
Status: #🌱 
Tags:
Links:
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
References: