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

two-way binding


two-way binding

for inputs we don't just listen to changes, but we can also pass a new value back into the input.

So that we can reset or change the input programmatically.

  

HTML attributes

`<input value="" />`

input.value => 設定預設值

  

  

because it allows you to gather user input, but then also change it.

For example, upon form of mission
## 複習

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]] - [[Rendering]]
Links:
[[HTML：form 標籤會有屬性、預設事件處理、如何觸發事件、提交]]
[[Data flow & Data binding 是指資料與UI之間的變動關係，分別為資料一變動、UI就跟著資料變動和UI一變動、資料就跟著UI變動]]
References:
