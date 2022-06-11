## 描述

[[@quamisWhatEagerLoading2012]] 描述：
> There are three levels:

> 1.  **Eager loading:** you do everything when asked. Classic example is when you multiply two matrices. You do all the calculations. That's eager loading;
> 2.  **Lazy loading:** you only do a calculation when required. In the previous example, you don't do any calculations until you access an element of the result matrix; and
> 3.  **Over-eager loading:** this is where you try and anticipate what the user will ask for and preload it.

> Let me give you a "Webby" example.

> Imagine a page with rollover images like for menu items or navigation. There are three ways the image loading could work on this page:

> 1.  Load every single image required before you render the page (**eager**);
> 2.  Load only the displayed images on page load and load the others if/when they are required (**lazy**); and
> 3.  Load only the displayed images on page load. After the page has loaded preload the other images in the background _in case you need them_ (**over-eager**).

[[@chuyi.inowEagerLoadingYuLazyLoading]] 描述：
> lazy loading指的是在用到該筆資料時才去動態載入，而與之相反的則是eager loading，顧名思義就是在用到資料前就先用sql語法取出存在變數中。

Eager loading：
- 是預先加載的意思，也就是在用到資料前就先去資料庫把會用到的資料A先取出來，存在特定空間中，接著等要用到的時候，直接從特定空間取出儲存結果來處理，而不是重複地向資料庫系統索要資料A

### eager loading example
理論案例：在這裏Eager loading會先處理B和處理function(C)來載入他們的值，接著等到正式做+時，就直接以結果進行相加

```
A = B + function(C)
```

### sequelize: Eager loading
[[@EagerLoadingSequelize]] 描述：
>  As briefly mentioned in [the associations guide](https://sequelize.org/docs/v6/core-concepts/assocs/), eager Loading is the act of querying data of several models at once (one 'main' model and one or more associated models). At the SQL level, this is a query with one or more [joins](https://en.wikipedia.org/wiki/Join_(SQL)).

> When this is done, the associated models will be added by Sequelize in appropriately named, automatically created field(s) in the returned objects.

> In Sequelize, eager loading is mainly done by using the `include` option on a model finder query (such as `findOne`, `findAll`, etc)

> - Earger loading 的 Sequelize 案例為：
  
```
const awesomeCaptain = await Captain.findOne({
	where: {
		name: "Jack Sparrow"
	},
	include: Ship
});

// Now the ship comes with it
console.log('Name:', awesomeCaptain.name);
console.log('Skill Level:', awesomeCaptain.skillLevel);
console.log('Ship Name:', awesomeCaptain.ship.name);
console.log('Amount of Sails:', awesomeCaptain.ship.amountOfSails);
```

重點：
- sequelize 可以觸發原生SQL上eager loading的語法會是include，只需要在各個讀取種類的操作(如findOne、findAll)添加options.include 就即可調用對應loading
```
Array<object|Model|string>
```

- sequelize find 系列的 include 語法是對應著SQL裡頭的 JOIN查詢，通常該查詢在對應資料庫系統中是以eager loading來處理
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]



### eager loading 命名緣由
- eager 表示當需求來臨時，強調某些人事物迫切地需要某些人事物
- loading 為載入資料，在這裡會是指向資料庫系統索要資料並成功獲取
- eager 搭配 loading 代表著當需求來臨時，迫切地需要某些人事物的 loading，或者指當需求來臨時，迫切地載入所有內容，而先預先載入會處理到的資料
## 複習
#🧠  Database: eager loading 命名緣由->->-> `eager 表示當需求來臨時，強調某些人事物迫切地需要某些人事物、loading 為載入資料，在這裡會是指向資料庫系統索要資料並成功獲取、eager 搭配 loading 代表著當需求來臨時，迫切地需要某些人事物的 loading，或者指當需求來臨時，迫切地載入所有內容，而先預先載入會處理到的資料`

#🧠 Database: eager loading 是什麼樣的技術(別說緣由) ->->-> `是預先加載的意思，也就是在用到資料前就先去資料庫把會用到的資料A先取出來，存在特定空間中，接著等要用到的時候，直接從特定空間取出儲存結果來處理，而不是重複地向資料庫系統索要資料A`

#🧠  以A = B + function(C)為例子來說明eager loading (提示：誰先執行？如何執行) ->->-> `在這裏Eager loading會先處理B和處理function(C)來載入他們的值，接著等到正式做+時，就直接以結果進行相加`


#🧠 Database：sequelize 如何在find系列操作觸發eager loading ->->-> `添加options.include就能觸發`

#🧠 sequelize find 系列的 include 語法 為何可以觸發eager loading? ->->-> `對應著SQL裡頭的 JOIN查詢，通常該查詢在對應資料庫系統中是以eager loading來處理`

---
Status: #🌱 
Tags: 
[[Database]] - [[Sequelize]] - [[ORM]]
Links:
[[Database - Lazy Loading 是當索求需求來臨時才會索求特定資料，且不會把結果儲存，其餘時間點都維持不執行索求]]
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]
References:
[[@EagerLoadingSequelize]]
[[@quamisWhatEagerLoading2012]]
[[@chuyi.inowEagerLoadingYuLazyLoading]]