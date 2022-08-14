
## 描述

> 使用 React element 處理事件跟使用 DOM element 處理事件是十分相似的。它們有一些語法上的差異：
> -   事件的名稱在 React 中都是 camelCase，而在 HTML DOM 中則是小寫。
> -   事件的值在 JSX 中是一個 function，而在 HTML DOM 中則是一個 string。


例如，在 HTML 中的語法：
```
<button onclick="activateLasers()">
	Activate Lasers
</button>
```

和在 React 中的語法有些微的不同：
```
<button onClick={activateLasers}>  
	Activate Lasers
</button>
```


JSX 為React Element提供事件綁定的API：
- 在指定元件的標籤上添加onXXXX屬性，後面接著function，XXXX 會是指事件名稱
- 這裡的onXXXX是react官方提供的語法
- 且轉換後的語法，也並不會實際直接以HTML方式來定義onClick，而是以JS來綁定





onClick 不用像HTML那樣要添加()

### onClick 夾雜的函式是否呼叫

```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler}></button>
)
```

若在JSX 語法中來呼叫clickHandler，會直接先執行clickHandler，並拿它回傳的內容來替代呼叫clickHandler，最後以那個內容來渲染。
```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler()}></button>
)
```


### 命名每個事件綁定的callback
```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler()}></button>
)
```


若沒特別命名法則來命名每個事件綁定的callback，那麼可以試著以 xxxx + Handler 來命名，其中xxxx為事件名稱。
```
const clickHandler = () => {
	.....
}
```

畢竟clickHandler最後會是由瀏覽器自己去幫忙執行，而非由React本身來處理


### 未變更對應元件內容的事件處理



```
function ExpenseItem(props) {

	let title = props.title;
	
	const clickHandler = () => {
		title = 'updated';
	};

return (
	<Card className='expense-item' id={props.id}>	
		<ExpenseDate date={props.date} />
		<div className='expense-item__description'>
			<h2>{title}</h2>
			<div className='expense-item__price'>{props.amount}</div>
		</div>
		<button onClick={clickHandler}>test btn</button>
	</Card>
);

}
```

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: