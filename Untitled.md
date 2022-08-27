


## 描述


### JSX 中{} 遇上陣列時
> as array of JSX elements as part of your JSX code, react would simply render elements side by side


JSX {}內 是以陣列來表示的話(如下)，

```
render(
	{[
		a,
		b,
		c,
	]}
)
```

會將陣列中的每個元素並排渲染著(如下)：
```
render (
	a
	b
	c
)
```

假若是存放著多個XML標籤所構成的陣列，那麼
```
render(
	{[
		<ExpenseItem
		  id={expenses[0].id}
		  title={expenses[0].title}
		  amount={expenses[0].amount}
		  date={expenses[0].date}>
		</ExpenseItem>
		,
		<ExpenseItem
		  id={expenses[1].id}
		  title={expenses[1].title}
		  amount={expenses[1].amount}
		  date={expenses[1].date}
		</ExpenseItem>
		,
		.
		.
		.
		.
	
	]}
)
```

會將陣列中的每個元素並排渲染著(如下)：
```
render(

		<ExpenseItem
		  id={expenses[0].id}
		  title={expenses[0].title}
		  amount={expenses[0].amount}
		  date={expenses[0].date}>
		</ExpenseItem>
		
		<ExpenseItem
		  id={expenses[1].id}
		  title={expenses[1].title}
		  amount={expenses[1].amount}
		  date={expenses[1].date}
		</ExpenseItem>
		.
		.
		.
		.
		.
)
```



rendering list & rendering conditional content

outputting dynamic lists of content


dynamic lists of content 
=> 在執行過程，根據執行時資訊來渲染內容




rendering content under certain conditions


## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-08-30,3,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: