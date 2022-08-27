

## 描述

### 為什麼需要Keys

special concept when it comes to rendering lists of data

a concept which exists to ensure that React is able to update and render such lists efficiently without performance losses, or bugs, which may occur.


當用來渲染的資料是陣列時，並使用陣列轉換成一組多個ExpenseItem元件來渲染，當對著陣列增加時

```
return (
	<div>
		<Card className='expenses'>
			<ExpensesFilter
			  selectedYear={year}
			  onChangeHandler={filterChangeHandler}
			/>
			
			{items.map((expense) => (
				<ExpenseItem
				  title={expense.title}
				  amount={expense.amount}
				  date={expense.date}
				/>
			))}
		</Card>
	</div>
);
```

當發生新增項目時，瀏覽器會是編輯著目前實際DOM結構


## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: