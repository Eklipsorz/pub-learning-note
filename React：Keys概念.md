

## 描述

### 為什麼需要Keys


### 為什麼需要Keys 案例


special concept when it comes to rendering lists of data

a concept which exists to ensure that React is able to update and render such lists efficiently without performance losses, or bugs, which may occur.


當用來渲染的資料是陣列時，並使用陣列轉換成一組多個ExpenseItem元件來轉換成實際DOM結構來渲染，

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

然而當對著陣列增加時，瀏覽器會是在存放ExpenseItem元件之清單最後頭增加一個項目，其中

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661608305/blog/react/dynamic-list-rendering/before-add-item-rendering-list-example_ehlrs2.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661608305/blog/react/dynamic-list-rendering/after-add-item-rendering-list-example_bumbfk.png)


最後一個項目的內容並不是新增內容，而是原本插入前的最後一個項目內容，最新新增內容是在清單第一個項目元素

原本項目為：
```
const DUMMY_EXPENSES = [
	{
		id: 'e1',
		title: 'Toilet Paper',
		amount: 94.12,
		date: new Date(2020, 7, 14),
	},
	{
		id: 'e2',
		title: 'New TV',
		amount: 799.49,
		date: new Date(2021, 2, 12),
	},
	{
		id: 'e3',
		title: 'Car Insurance',
		amount: 294.67,
		date: new Date(2021, 2, 28),
	},
	{
		id: 'e4',
		title: 'New Desk (Wooden)',
		amount: 450,
		date: new Date(2021, 5, 12),
	},
];
```


第一個項目：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661608857/blog/react/dynamic-list-rendering/add-item-to-list-example-first-item_eyf97r.png)


最後一個元素：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661608857/blog/react/dynamic-list-rendering/add-item-to-list-example-last-item_j9vbez.png)


#### 結論：為什麼需要Keys 案例

> update all items and replace their content such that it again matches the order of the items in my Array and this is not great. because to React all these items look similar and it only sees that my Array changed that it's not longer than before. And hence it simply renders an additional div and it adds that at the end. And then it simply walks through all the items and updates the content inside of every item to match the Array content again

當新增項目時，觀察到：
1. 清單會增加一個項目的對應DOM結構
2. 清單內的第一個項目的內容會是新增項目的內容
3. 清單內的項目會是依照舊有項目內容往下移動的結果

當發生新增項目時，React的清單實際上是處於生命週期的updating階段，這階段會是：
1. 比較現在Virtual DOM結構和目前Virtual DOM結構之間的差異
2. 以差異來轉換成對應實際DOM結構的對應指令

當執行指令時，具體會在清單內
1. 增加一個清單項目的對應DOM項目
2. 並對著每個清單項目重新拜訪並依據目前陣列內容來填寫每個項目的內容




預期效果會是：
1. 新增一個項目並存放最新內容
2. 將新增項目插入至清單的第一個位置

無法實現是因為系統無法判別哪一個項目


## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: