

- 在 sequelize 中的 Lazy loading 則是指的先用到的資料不會先用 SQL 語法取出並放入特定空間，而是等到真正需要存取該資料的時候才會用 SQL 語法去處理

  

- 理論案例：在這裏Lazy loading會從B開始處理，接著處理function(C)並載入其回傳值，最後再拿B和function(C)進行相加，不會像Eager loading先處理獲取B和載入function(C)的回傳值

```
A = B + function(C)
```

- Lazy loading 的 Sequelize 案例為：
```
const awesomeCaptain = await Captain.findOne({
	where: {
		name: "Jack Sparrow"
	}
});

// Do stuff with the fetched captain
console.log('Name:', awesomeCaptain.name);
console.log('Skill Level:', awesomeCaptain.skillLevel);

// Now we want information about his ship!
const hisShip = await awesomeCaptain.getShip();

// Do stuff with the ship
console.log('Ship Name:', hisShip.name);
console.log('Amount of Sails:', hisShip.amountOfSails);
```

  

## 描述

[[@martingibbsWhatQuerySQL]] 所描述：
> A **query** is really a question or request for data. For example, ''Tell me how many books there are on computer programming'' or ''How many Rolling Stones albums were produced before 1980?'' When we query databases, we can use a common language to get the information. **Structured Query Language SQL)**, is a fairly universal language. There are some different flavors, but once you know the basics you can easily adapt your questions.

[[@wikidataSQL2022]] 所描述：
> The scope of SQL includes data query, data manipulation (insert, update and delete), data definition ([schema](https://en.wikipedia.org/wiki/Database_schema "Database schema") creation and modification), and data access control. Although SQL is essentially a [declarative language](https://en.wikipedia.org/wiki/Declarative_programming "Declarative programming") ([4GL](https://en.wikipedia.org/wiki/4GL "4GL")), it also includes [procedural](https://en.wikipedia.org/wiki/Procedural_programming "Procedural programming") elements.


重點：
- Lazy loading 是索求需求來臨時才會索求特定資料，且不會把結果儲存，其餘時間點都維持不執行索求或者保持懶惰。
- 


### Lazy Loading 命名緣由
- Lazy 是指懶惰的，被動的，在這裡是指除了真正需要，否則什麼都不做
- Loading 是指載入資料，在這裡會是指向資料庫索要資料並成功獲取
- Lazy 強調 Loading是相對於Eagerly Loading或者Eager loading，當需求來臨時，才會去做載入資料，否則就保持懶惰，什麼都不做


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Databse]] - [[Sequelize]] - [[ORM]]
Links:
[[Database - Eager loading 是指主動索求未來會用到的資料集合並將結果放入特定空間，然後透過儲存結果來處理，以減緩不必要的處理]]
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]
References:
[[@quamisWhatEagerLoading2012]]
[[@EagerLoadingSequelize]]
[[@chuyi.inowEagerLoadingYuLazyLoading]]