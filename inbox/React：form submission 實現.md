## 描述


### 當發生提交事件時，如何提交資料

要求：
- 發生事件，就將資料傳遞至指定位置
- 傳遞後，清除掉輸入欄上的目前所填寫之資料

#### 方法1

##### 發生事件，就將資料傳遞至指定位置
不擷取存放資料區塊的DOM節點，直接擷取每一次輸入的內容，並挑最後內容作為提交的最終版本


```
const titleChangeHandler = (event) => {
	const title = event.target.value;
	setEnteredTitle(title);
};
```

```
const amountChangeHandler = (event) => {
	const amount = event.target.value;
	setEnteredAmount(amount);
};
```

```
const dateChangeHandler = (event) => {
	const date = event.target.value;
	setEnteredDate(date);
};
```


```
const submitHandler = (event) => {
	event.preventDefault();
	event.stopPropagation();
		
	const expenseData = {
		title: enteredTitle,
		amount: enteredAmount,
		date: new Date(enteredDate),
	};
	
	console.log(expenseData);
};
```

```
return (
	<form onSubmit={submitHandler}>
		<input type='text' onChange={titleChangeHandler}></input>
		<input type='text' onChange={amountChangeHandler}></input>
		<input type='text' onChange={dateChangeHandler}></input>
	</form>
);
```

##### 傳遞後，清除掉輸入欄上的目前所填寫之資料

直接以更新狀態用的函式來刷新對應的輸入欄位，其中畫面渲染部分使用每個input元件上的value屬性來填入空字串，表示清除掉：
	- 當發生提交事件就執行setState('')來要更新title、amount、date
	- 重新渲染後，就將新title、amount、date填入每個input元件上的value以示清空
```
const submitHandler = (event) => {

	event.preventDefault();
	event.stopPropagation();
	
	const expenseData = {
		title: enteredTitle,
		amount: enteredAmount,
		date: new Date(enteredDate),
	};
	
	setEnteredTitle('');
	setEnteredAmount('');
	setEnteredDate('');

};
```


```
return (
	<form onSubmit={submitHandler}>
		<div>
			<input 
			  type='date'
			  min='2019-01-01'
			  max='2022-12-31'
			  value={enteredDate}
			  onChange={dateChangeHandler} 
			 ></input>
		</div>
		<div>
			<input
			  type='text'
			  value={enteredTitle}
			  onChange={titleChangeHandler}
			 ></input>
		</div>
		<div>
			<input
			  type='number'
			  min='0.01'
			  step='0.01'
			  value={enteredAmount}
			  onChange={amountChangeHandler}
			 ></input>
		</div>
	</form>
);
```


### one-way：UI一改變，資料就跟著改變
在這裡是以元件來攔截使用者所輸入的資訊，而目前資料/Data Model並沒有這資訊，因此從攔截並成為Data Model的一部分，會等同於UI(UI上的輸入欄位)一改變，資料就跟著改變
```
const submitHandler = (event) => {
	event.preventDefault();
	event.stopPropagation();
	
	const expenseData = {
		title: enteredTitle,
		amount: enteredAmount,
		date: new Date(enteredDate)
	};
};
```


```
return (
	<form onSubmit={submitHandler}>
		<input type='text' onChange={titleChangeHandler}></input>
		<input type='text' onChange={amountChangeHandler}></input>
		<input type='text' onChange={dateChangeHandler}></input>
	</form>
);
```

### one-way：資料一改變，UI就跟著改變
在這裡是要求每個輸入欄位為''，所以才以setState來間接引發渲染，進而以新資料來渲染。
```
const submitHandler = (event) => {

	event.preventDefault();
	event.stopPropagation();
	
	const expenseData = {
		title: enteredTitle,
		amount: enteredAmount,
		date: new Date(enteredDate),
	};
	
	setEnteredTitle('');
	setEnteredAmount('');
	setEnteredDate('');

};
```


```
return (
	<form onSubmit={submitHandler}>
		<div>
			<input 
			  type='date'
			  min='2019-01-01'
			  max='2022-12-31'
			  value={enteredDate}
			  onChange={dateChangeHandler} 
			 ></input>
		</div>
		<div>
			<input
			  type='text'
			  value={enteredTitle}
			  onChange={titleChangeHandler}
			 ></input>
		</div>
		<div>
			<input
			  type='number'
			  min='0.01'
			  step='0.01'
			  value={enteredAmount}
			  onChange={amountChangeHandler}
			 ></input>
		</div>
	</form>
);
```


## 複習
#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，請問要如何實現用React程式碼去實現提交就獲取資訊並清空欄位值？ ->->-> ``
<!--SR:!2022-09-22,15,228-->

#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，在React概念上來說，要如何實現表單的獲取資訊？(共有兩個方法) ->->-> `當輸入欄位發生change事件時就擷取內容、獲取對應DOM元件來獲取值`
<!--SR:!2022-09-21,16,230-->

#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，在React概念上來說，為何要用**當輸入欄位發生change事件時就擷取內容，而非以獲取對應DOM元件來獲取值** 實現表單的獲取資訊？->->-> `這是若直接改以獲取對應DOM元件來獲取值的話，未來會很難控管表單元件的狀態和狀態對應話渲染`
<!--SR:!2022-09-20,16,248-->

#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，在data-binding概念上來說，透過互動來接收資訊會屬於哪種binding，為什麼？->->-> `屬於UI一變動，資料就跟著UI變動而跟著變動，原因為資訊是從互動而得到。`
<!--SR:!2022-10-07,28,250-->

#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，在data-binding概念上來說，透過互動來清除欄位會屬於哪種binding，為什麼？->->-> `屬於資料一變動，UI就跟著資料變動而跟著變動，雖然是發生特定互動才清除，但實際上這些欄位值是可以綁定著狀態來變動的話，那麼實際上就是指示''空字串，並根據空字串來渲染`
<!--SR:!2022-10-26,37,248-->

#🧠 假設要建立一個表格，主要會有填入日期、標題、價格的輸入欄位、提交按鈕、當提交時，在React概念上來說，要如何實現表單發交提交就清除欄位值？->->-> `具體先用狀態來綁定每個輸入欄位，並且事件處理那裡指定setState('')就能夠實現`
<!--SR:!2022-10-19,34,248-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]] - [[Rendering]]
Links:
[[HTML：form 標籤會有屬性、預設事件處理、如何觸發事件、提交]]
[[Data flow & Data binding 是指資料與UI之間的變動關係，分別為資料一變動、UI就跟著資料變動和UI一變動、資料就跟著UI變動]]
[[原生HTML DOM元件都會有瀏覽器根據標準而開發出來的原生狀態管理實現，分別是將元件轉換成DOM物件來儲存狀態以及設定預設事件處理來變更狀態和渲染內容]]
References:
