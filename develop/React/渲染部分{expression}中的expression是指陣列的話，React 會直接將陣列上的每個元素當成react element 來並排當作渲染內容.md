


## 描述

渲染部分{expression}中的expression是指陣列的話，React會如何解析？
1. React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容


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
#🧠 React：渲染部分{expression}中的expression是指陣列的話，React會如何解析？->->-> `React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容`
<!--SR:!2022-10-05,25,250-->

#🧠 React：請問React如何解析這表達式，請用程式碼來表示![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661681064/blog/react/dynamic-list/simple-array-example_hlcaww.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661681064/blog/react/dynamic-list/simple-array-result_cxugsx.png)`
<!--SR:!2022-10-05,25,250-->

#🧠 React：請問React如何解析這表達式，請用程式碼來表示 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661681064/blog/react/dynamic-list/expense-array-example_wqhppu.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661681064/blog/react/dynamic-list/expense-array-to-template-example_q1bhds.png)`
<!--SR:!2022-09-28,20,250-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：render 函式能夠回傳的JSX Element可以是一般的JSX Element、條件式、陣列形式的JSX Element]]
[[Each child in a list should have a unique "key" prop. 表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點]]
References: