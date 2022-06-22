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
> lazy loading指的是在用到該筆資料時才去載入，而與之相反的則是eager loading，顧名思義就是在用到資料前就先用sql語法取出存在變數中。

Eager loading：
- 當請求來時，會直接載入所有內容，這些內容會包含著請求要的目標內容和未來會用到的內容，而未來會用到的內容通常會是與目標內容相關的內容。
- 資料庫接收到索求特定資料的請求時，就會直接載入所有資料給客戶端，而所有資料會泛指著特定資料、與資料相關的資料、未來會用到的資料，而非真是資料庫上的所有資料`
> **Eager loading:** you do everything when asked.

Lazy loading： 
- 當請求來時，只會按照請求的目標內容來載入，不會載入還沒用到的內容
> **Lazy loading:** you only do a calculation when required.


### eager loading example

> -   Load every single image required before you render the page (**eager**);
> -   Load only the displayed images on page load and load the others if/when they are required (**lazy**)

假如有個導覽列，當被點開的時候，會呈現三個用圖片做成的選項；當沒被點開的時候，不會呈現三個選項。在這裡，若是eager loading的話，不管有沒有點開，都會先載入那三個選項，然後最後呈現時就直接呈現



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
-  案例說明：假設會有船長表格和船表格，在sequelize eager loading中，會先向資料庫索取船表格並儲存在名為Ship的儲存空間，然後再從船長表格取出資料來遍歷每個船長來從傳的儲存結果找到對應的船資訊
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


### eager loading 命名緣由
- eager 意指為對某個東西而感到非常想要
> **wanting** **very much to do or have something, especially something interesting or enjoyable**
-  loading 意指為將一批東西裝入裝置的動作
> **to put a lot of things into a vehicle or machine**
- eager loading 兩字合併起來就是對某個東西感到迫切需要而做的東西載入動作，在這裡會是形容資料庫系統，會是形容該系統一接收到請求，就會表現出迫切需求的態度將所有資料都一併載入，而這裡的所有資料是指著目標資料、與資料相關的資料、未來會用到的資料，並非真的就是資料庫系統的所有資料，最後回傳給客戶端
## 複習
#🧠  Database: eager loading 命名緣由->->-> `- eager 意指為對某個東西而感到非常想要 - loading 意指為將一批東西裝入裝置的動作 - eager loading 兩字合併起來就是對某個東西感到迫切需要而做的東西載入動作，在這裡會是形容資料庫系統，會是形容該系統一接收到請求，就會表現出迫切需求的態度將所有資料都一併載入，而這裡的所有資料是指著目標資料、與資料相關的資料、未來會用到的資料，並非真的就是資料庫系統的所有資料，最後回傳給客戶端`


#🧠 Database: eager loading 是什麼樣的技術(別說緣由) ->->-> `資料庫接收到索求特定資料的請求時，就會直接載入所有資料給客戶端，而所有資料會泛指著特定資料、與資料相關的資料、未來會用到的資料，而非真是資料庫上的所有資料`

#🧠 資料庫系統若採用 eager loading  的話，其資料會是由什麼構成 (提示：目標資料和xxx) ->->-> `資料庫系統會是回傳目標資料和與目標資料相關的資料`

#🧠  假如有個導覽列，當被點開的時候，會呈現三個用圖片做成的選項；當沒被點開的時候，不會呈現三個選項 ，試說明Eager loading ->->-> `在這裡，若是eager loading的話，不管有沒有點開，都會先載入那三個選項，然後最後呈現時就直接呈現`
<!--SR:!2022-06-24,10,250-->


#🧠 Database：sequelize 如何在find系列操作觸發eager loading ->->-> `添加options.include就能觸發`
<!--SR:!2022-06-23,9,250-->

#🧠 sequelize find 系列的 include 語法 為何可以觸發eager loading? ->->-> `對應著SQL裡頭的 JOIN查詢，通常該查詢在對應資料庫系統中是以eager loading來處理`
<!--SR:!2022-06-24,10,250-->

#🧠 請使用eager loading來說明sequelize這段語法(提示：船和船長) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654935202/blog/database/orm/sequelize-eager-loading-example_k9neij.png)->->-> `案例說明：假設會有船長表格和船表格，在sequelize eager loading中，會先向資料庫索取船表格並儲存在名為Ship的儲存空間，然後再從船長表格取出資料來遍歷每個船長來從傳的儲存結果找到對應的船資訊`
<!--SR:!2022-07-09,18,250-->


---
Status: #🌱 
Tags: 
[[Database]] - [[sequelize]] - [[ORM]]
Links:
[[Database - Lazy Loading 是當索求需求來臨時才會索求特定資料，且不會把結果儲存，其餘時間點都維持不執行索求]]
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]
References:
[[@EagerLoadingSequelize]]
[[@quamisWhatEagerLoading2012]]
[[@chuyi.inowEagerLoadingYuLazyLoading]]