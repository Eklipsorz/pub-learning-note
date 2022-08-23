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



### 

## 複習

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]] - [[Rendering]]
Links:
[[HTML：form 標籤會有屬性、預設事件處理、如何觸發事件、提交]]
[[Data flow & Data binding 是指資料與UI之間的變動關係，分別為資料一變動、UI就跟著資料變動和UI一變動、資料就跟著UI變動]]
References:
