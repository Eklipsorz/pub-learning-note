Eager loading：

 
- eager 表示當需求來臨時，強調某些人事物迫切地需要某些人事物，搭配 loading 代表著當需求來臨時，迫切地需要某些人事物的 loading，或者指當需求來臨時，迫切地載入所有內容，

- 在 sequelize 中的 Eager loading 則是指的先用到的資料先用 SQL 語法取出並放入特定空間，好與其他資料進行處理。

- eager loading，是預先加載的意思，也就是在用到資料前就先去資料庫把資料取出來，存在變數中。

- 理論案例：在這裏Eager loading會先處理B和處理function(C)來載入他們的值，接著等到正式做+時，就直接以結果進行相加

```
A = B + function(C)
```

- Earger loading 的 Sequelize 案例為：

  
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


### sequelize - eager loading
>  As briefly mentioned in [the associations guide](https://sequelize.org/docs/v6/core-concepts/assocs/), eager Loading is the act of querying data of several models at once (one 'main' model and one or more associated models). At the SQL level, this is a query with one or more [joins](https://en.wikipedia.org/wiki/Join_(SQL)).

> When this is done, the associated models will be added by Sequelize in appropriately named, automatically created field(s) in the returned objects.

> In Sequelize, eager loading is mainly done by using the `include` option on a model finder query (such as `findOne`, `findAll`, etc)

https://sequelize.org/docs/v6/advanced-association-concepts/eager-loading/


options.include，其參數可填入

```
Array<object|Model|string>
```


- [what-is-eager-loading](https://stackoverflow.com/questions/1299374/what-is-eager-loading)

- [eager-loading-and-lazy-loading](https://chuyi.inow.tw/2013/02/eager-loading-and-lazy-loading/)


## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: #📥 
Tags: 
[[Database]] 
Links:
[[Database - Lazy Loading 是當索求需求來臨時才會索求特定資料，且不會把結果儲存，其餘時間點都維持不執行索求]]
References:
