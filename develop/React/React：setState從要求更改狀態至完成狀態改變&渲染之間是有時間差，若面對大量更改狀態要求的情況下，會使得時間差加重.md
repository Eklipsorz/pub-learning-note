

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

### 若要求更改的狀態和目前狀態一致的話

狀態檢查方式：
- 狀態為primitive data value，那麼就以識別字所對應的stack 記憶體區塊的內容來比較，也就是要求更改的狀態和目前狀態之間的比較就以data value本身來比較
- 狀態為object，那麼就以識別字所對應的stack 記憶體區塊的內容來比較，其內容會是物件所在的Heap記憶體區塊位址，也就是要求更改的狀態和目前狀態之間的比較就以Heap 記憶體區塊位址比較


若是狀態一樣的話
1. 若要求更改的狀態內容和目前狀態內容之間的比較結果是一樣的，那麼則判斷為毫無變化，React因而不做多餘的狀態更新和渲染


## 複習

#🧠 React：請問每當執行setState會立即更改狀態&渲染嗎？還是有時間差？為什麼？ ->->-> `在執行setState時並不會立即改變狀態&渲染並刷新state值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**，這使得從要求更改狀態至完成狀態改變&渲染之間是有時間差`
<!--SR:!2024-01-28,313,250-->

#🧠 React：請問每次執行setState時，從要求更改狀態至完成狀態改變&渲染之間是有時間差，具體是為什麼？ ->->->`在執行setState時並不會立即改變狀態&渲染並刷新state值，而是**先將目前接收到的狀態先與過去的狀態合併，接著等到確定沒狀態更新指令時才會正式立即改變狀態&渲染**`
<!--SR:!2023-12-16,103,230-->

#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行setState所得到的時間差會變成如何 ->->-> `時間差會使要求逐漸累績起來，進而加重時間差`
<!--SR:!2023-06-03,173,250-->


#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行State所得到的時間差會被加重，假如setState1的狀態本身是以物件來表示且state1是源自於其他useState所負責的狀態，那麼現在對於setState1({...state1, a})所回傳的值來說會有什麼潛在問題? 為什麼(以依賴、渲染來說明)->->-> `主要是不一致的問題，由於狀態都是依賴著state1來更改，state1是必須透過渲染才能拿到最新狀態，然而在時間加重到無法透過渲染更新狀態，目前state1很有可能會是較舊，若中間有部分資料要更新的話`
<!--SR:!2023-08-08,192,250-->



#🧠 React：若面對大量更改狀態要求的情況下，對於每次執行State所得到的時間差會被加重，假如setState1的狀態本身是以物件來表示)且state1是源自於setState1所負責的狀態所回傳的值，現在對於setState1({...state1', a})的state會有內容老舊的問題，那麼解法會是什麼？ ->->-> `使用callback當作setState參數，並用callback來取得較新的狀態state1`
<!--SR:!2023-06-10,61,230-->



#🧠 React：setState 的狀態檢查方式，若狀態為primitive data value，會如何比對狀態之間的差異？->->-> `狀態為primitive data value，那麼就以識別字所對應的stack 記憶體區塊的內容來比較，也就是要求更改的狀態和目前狀態之間的比較就以data value本身來比較`
<!--SR:!2024-08-02,407,250-->


#🧠 React：setState 的狀態檢查方式，若狀態為object，會如何比對狀態之間的差異？ ->->-> `狀態為object，那麼就以識別字所對應的stack 記憶體區塊的內容來比較，其內容會是物件所在的Heap記憶體區塊位址，也就是要求更改的狀態和目前狀態之間的比較就以Heap 記憶體區塊位址比較`
<!--SR:!2024-06-10,296,230-->


#🧠 React：setState 的狀態檢查方式，若狀態為primitive data value，會拿什麼內容來代表狀態進行比較差異？->->-> `也就是要求更改的狀態和目前狀態之間的比較就以data value本身來比較`
<!--SR:!2023-07-22,182,250-->

#🧠 React：setState 的狀態檢查方式，若狀態為object，會拿什麼內容來代表狀態進行比較差異？->->-> `識別字所對應的stack 記憶體區塊的內容來比較，其內容會是物件所在的Heap記憶體區塊位址，也就是要求更改的狀態和目前狀態之間的比較就以Heap 記憶體區塊位址比較`
<!--SR:!2024-08-09,403,250-->


#🧠 React：setState 的狀態檢查方式，若要求更改的狀態和目前狀態一樣的話？會發生什麼 ->->-> `若要求更改的狀態內容和目前狀態內容之間的比較結果是一樣的，那麼則判斷為毫無變化，React因而不做多餘的狀態更新和渲染`
<!--SR:!2024-02-14,300,250-->


#🧠 React：setState 的狀態檢查方式，若狀態是物件，如何作才能讓狀態比對結果為一樣 ->->-> `使用相同的Heap記憶體區塊位址`
<!--SR:!2024-12-25,493,250-->

#🧠 React：setState 的狀態檢查方式，若狀態是primitive data value，如何作才能讓狀態比對結果為一樣 ->->-> `使用相同的primitive data value`
<!--SR:!2025-01-18,502,250-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
References: