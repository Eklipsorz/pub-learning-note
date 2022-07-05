
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


重點：
-  Lazy loading 是當資料庫接收索求資料的請求時，只會載入請求所要的目標資料，不會載入沒指定的內容，即使是與內容相關的資料也是一樣。

### Lazy loading example

> -   Load every single image required before you render the page (**eager**);
> -   Load only the displayed images on page load and load the others if/when they are required (**lazy**)

假如有個導覽列，當被點開的時候，會呈現三個用圖片做成的選項；當沒被點開的時候，不會呈現三個選項。在這裡，若是lazy loading的話，會按照是否點開來載入那三個選項才呈現，若點開就載入，若不點開就不載入



### Lazy Loading 命名緣由
- Lazy 是指懶惰的，被動的，通常會與某個對象比較，在這裡會是與eager loading比較，指了只做真正需要的，不會做額外的事情，即使是是未來會出現的。
- Loading 是指載入資料
- Lazy 強調 Loading是相對於Eagerly Loading或者Eager loading，兩字合併起來就是 只做真正需要載入的載入，不會做不需要的載入工作。 當需求來臨時，只會載入需求想要的內容A，不會額外載入與需求不需要的內容B，甚至該內容B與內容A是相關，也不會額外載入。



### Sequelize: Lazy Loading
在 sequelize 中的 Lazy loading 則是指的先用到的資料不會先用 SQL 語法取出並放入特定空間，而是等到真正需要存取該資料的時候才會用 SQL 語法去處理


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

假如有船和船長表格，一開始會索要船長表格上的資訊，那麼就回傳其資訊，直到需要船長相關的船資訊，那麼就會從船表格找到與該船長相關的船，在這裡會是由getShip來實現，接著從船資訊來回傳

其中getShip 是sequelize 自動添加至船長實例的方法，主要回傳船長相關連的船資訊
> Note: the `getShip()` instance method used above is one of the methods Sequelize automatically adds to `Captain` instances. There are others. You will learn more about them later in this guide.




## 複習
#🧠  假如有個導覽列，當被點開的時候，會呈現三個用圖片做成的選項；當沒被點開的時候，不會呈現三個選項 ，試說明Lazy loading ->->-> `假如有個導覽列，當被點開的時候，會呈現三個用圖片做成的選項；當沒被點開的時候，不會呈現三個選項。在這裡，若是lazy loading的話，會按照是否點開來載入那三個選項才呈現，若點開就載入，若不點開就不載入`
<!--SR:!2022-07-17,24,250-->

#🧠  Database：Lazy Loading 命名緣由 （提示：lazy是懶惰，但是是相對於哪種loading的懶惰)->->->`- Lazy 是指懶惰的，被動的，通常會與某個對象比較，在這裡會是與eager loading比較，指了只做真正需要的，不會做額外的事情，即使是是未來會出現的。 - Loading 是指載入資料 - Lazy 強調 Loading是相對於Eagerly Loading或者Eager loading，兩字合併起來就是 只做真正需要載入的載入，不會做不需要的載入工作。 當需求來臨時，只會載入需求想要的內容A，不會額外載入與需求不需要的內容B，甚至該內容B與內容A是相關，也不會額外載入。`
<!--SR:!2022-07-30,25,250-->


#🧠 試著用Lazy Loading 來說明 sequelize 語法 (提示：船和船長) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654935600/blog/database/orm/sequelize-lazy-loading-example_kumr5g.png)->->-> `假如有船和船長表格，一開始會索要船長表格上的資訊，那麼就回傳其資訊，直到需要船長相關的船資訊，那麼就會從船表格找到與該船長相關的船，在這裡會是由getShip來實現，接著從船資訊來回傳`
<!--SR:!2022-07-31,31,248-->

#🧠 Database：Lazy Loading 是什麼？->->-> `Lazy loading 是當資料庫接收索求資料的請求時，只會載入請求所要的目標資料，不會載入沒指定的內容，即使是與內容相關的資料也是一樣。`
<!--SR:!2022-08-02,28,250-->






---
Status: #🌱 
Tags:
[[Database]] - [[sequelize]] - [[ORM]]
Links:
[[Database - Eager loading 是指主動索求未來會用到的資料集合並將結果放入特定空間，然後透過儲存結果來處理，以減緩不必要的處理]]
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]
References:
[[@quamisWhatEagerLoading2012]]
[[@EagerLoadingSequelize]]
[[@chuyi.inowEagerLoadingYuLazyLoading]]