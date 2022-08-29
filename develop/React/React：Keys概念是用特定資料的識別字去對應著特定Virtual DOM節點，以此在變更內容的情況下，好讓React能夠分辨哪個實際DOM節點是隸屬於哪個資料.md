

## 描述

### 需要Keys


> if you wonder what you do, if you have no unique ID：
> 1. 別使用map的callback上的第二參數index來當作ID
> 2. 使用明確且獨特的id



> Key 幫助 React 分辨哪些項目被改變、增加或刪除。在 array 裡面的每個 element 都應該要有一個 key，如此才能給予每個 element 一個固定的身份：


Keys 主要用途為：
- 用代表特定資料的識別字去對Virtual DOM和對應的實際DOM結構進行綁定，好方便判別哪些DOM節點對應哪些特定資料是被改變、增加或者移除

只要讓系統能夠判別哪些DOM節點對應哪些特定資料的話，就能讓React針對需要處理的DOM節點來進行，而非是特定範圍內的所有DOM節點來進行

當進行綁定會如同下圖：
- 每個對應DOM節點都利用id來進行綁定
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661613698/blog/react/dynamic-list-rendering/before-vs-after-with-keys_cedmf3.png)

#### 具體如何使用

在對應component添加key屬性，其屬性值為對應某種資料的識別字：
```
<Component key=identifier1 />
```

identifier1 可以是：
1. 字串、數字
2. 建議要使用獨特且不重複
3. 別使用map所產生的index來搭配

#### Keys 概念的適用場景
1. 開發清單的CRUD

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
1. 清單會增加一個DOM結點
2. 清單內的第一個DOM節點的內容會是新增項目的內容
3. 清單內的剩下DOM節點會是依照舊有DOM節點內容往下移動的結果

當發生新增項目時，React的清單實際上是處於生命週期的updating階段，這階段會是：
1. 比較現在Virtual DOM結構和目前Virtual DOM結構之間的差異
2. 以差異來轉換成對應實際DOM結構的對應指令

當執行指令時，具體會在清單內
1. 增加一個DOM節點至
2. 並對著每個DOM節點重新拜訪並依據目前陣列內容來填寫每個項目的內容




預期效果會是：
1. 新增一個DOM節點並存放最新內容
2. 將新增的DOM節點插入至清單的第一個位置

就預期效果的實現來說，是無法實現，原因會是由於不知道每個清單項目的對應DOM結構是與哪個資料做綁定，就如同下圖中的before那樣，每個灰球都代表著對應清單的實際DOM節點，React由於在這些節點無法判別哪個節點歸屬於哪個資料，就只好拜訪每個紀錄來填寫項目。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661613698/blog/react/dynamic-list-rendering/before-vs-after-with-keys_cedmf3.png)

所以只要一新增項目，在不清楚哪個清單項目是與哪個狀態進行綁定的情況下，會選擇做：
1. 新增一個實際DOM節點
2. 對每個實際DOM節點進行拜訪，然後按照順序填寫資料給這些節點

#### 為什麼React 不知道每個清單項目的對應DOM結構是與哪個資料做綁定

1. Virtual DOM節點 預設會對應著實際DOM節點
2. 資料 預設並不會對應Virtual DOM節點



#### 造成的問題？
1. 效能問題：每次新增都需要重新對整份清單渲染，而非針對新增的項目
2. 原有DOM節點上的狀態註冊會繼續保留在原有DOM節點上，不會根據實際轉換的位置來重新撤銷和註冊，比如說以下面內容來建立清單項目，其中Toilet Paper被註冊了特定狀態，那麼就表示對應該內容的第一個DOM節點會註冊那個狀態1，而當新資料進來時，第一個DOM節點內容會是新資料，而第二個DOM節點內容才是Toilet Paper，其中狀態1仍註冊在第一個DOM節點，而非轉移至第二個DOM節點。

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

## 複習
#🧠 React：Keys 主要用途是什麼？ ->->-> `用代表特定資料的識別字去對Virtual DOM和對應的實際DOM結構進行綁定，好方便判別哪些DOM節點對應哪些特定資料是被改變、增加或者移除`

#🧠 React：Keys 是用代表特定資料的識別字去對Virtual DOM和對應的實際DOM結構進行綁定，其好處是什麼？ ->->-> `只要讓系統能夠判別哪些DOM節點對應哪些特定資料的話，就能讓React針對需要處理的DOM節點來進行，而非是特定範圍內的所有DOM節點來進行`

#🧠 React：當對著Virtual DOM設定Keys，那麼其實際DOM節點會是？ ->->-> `也會因此對應著特定資料。`
<!--SR:!2022-09-01,3,250-->

#🧠 React：Keys概念的適用場景為何？ ->->-> `開發清單的CRUD`
<!--SR:!2022-08-30,1,230-->


#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，能從實際DOM結構發現什麼？->->-> `1. 清單會增加一個DOM結點 2. 清單內的第一個DOM節點的內容會是新增項目的內容 3. 清單內的剩下DOM節點會是依照舊有DOM節點內容往下移動的結果
`

#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，對於整份清單而言會是處於什麼樣的生命週期？ ->->-> `updating`
<!--SR:!2022-09-01,3,250-->

#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，具體會是做什麼來實現新元素的渲染？(不用談論結構) ->->-> `1. 增加一個DOM節點至 2. 並對著每個DOM節點重新拜訪並依據目前陣列內容來填寫每個項目的內容`
<!--SR:!2022-09-01,3,250-->


#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，預期效果會是如何？ ->->-> `1. 新增一個DOM節點並存放最新內容 2. 將新增的DOM節點插入至清單的第一個位置`


#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，是新增DOM項目至清單並且重新渲染整份清單，為何不是針對新增的項目來渲染？ ->->-> `原因會是由於不知道每個清單項目的對應DOM結構是與哪個資料做綁定`

#🧠 React：未使用Keys之前，為什麼React 不知道每個清單項目的對應DOM結構是與哪個資料做綁定->->-> `Virtual DOM節點 預設會對應著實際DOM節點、資料 預設並不會對應Virtual DOM節點`

#🧠 React：未使用Keys之前，在面對React 不知道每個清單項目的對應DOM結構是與哪個資料做綁定，React如何實現新增項目至清單的？ ->->-> `直接新增一個DOM節點，並且對每個實際DOM節點進行拜訪，然後按照順序填寫資料給這些節點`
<!--SR:!2022-09-01,3,250-->


#🧠 React：未使用Keys之前，一份4個元素的清單項目已經插入至實際DOM結構，那麼對著其清單加入新元素時，會有什麼潛在問題嗎？ ->->-> ` 效能問題：每次新增都需要重新對整份清單渲染，而非針對新增的項目、原有DOM節點上的狀態註冊會繼續保留在原有DOM節點上，不會根據實際轉換的位置來重新撤銷和註冊`
<!--SR:!2022-08-31,2,248-->


#🧠 React：未使用Keys之前會有潛在問題之一：原有DOM節點上的狀態註冊會繼續保留在原有DOM節點上，不會根據實際轉換的位置來重新撤銷和註冊，舉例說明一下 ->->-> `以兩個項目內容的清單來說明，其中第一個項目Toilet Paper被註冊了特定狀態，那麼就表示對應該內容的第一個DOM節點會註冊那個狀態1，而當新資料進來時，第一個DOM節點內容會是新資料，而第二個DOM節點內容才是Toilet Paper，其中狀態1仍註冊在第一個DOM節點，而非轉移至第二個DOM節點。`
<!--SR:!2022-09-01,3,250-->


#🧠 React：最左邊是要插入的資料，Before是實際建立的DOM節點，目前按照順序填入資料，After 是使用Keys技術，請詳細說明使用之後的概念![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661613698/blog/react/dynamic-list-rendering/before-vs-after-with-keys_cedmf3.png) ->->-> ``


#🧠 React：如何使用Keys概念至Virtual DOM節點上？ 語法形式如何？->->-> `在對應component添加key屬性，其屬性值為對應某種資料的識別字：<Component key=identifier1 />`

#🧠 React：使用\<Component key=identifier1 \/\> 來設定Component 對應著identifier1所對應的資料，那麼identifier1 主要是什麼？ 可填入什麼 ->->-> `主要是每個資料的識別字，可以填入字串、數字`

#🧠 React：使用\<Component key=identifier1 \/\> 來設定Component 對應著identifier1所對應的資料，那麼identifier1  使用map所產生的index來搭配 會有什麼問題？ ->->-> `會因為index並不會根據資料而跟著變動，只是按照順序分配，所以仍會有效能、狀態註冊問題`


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: