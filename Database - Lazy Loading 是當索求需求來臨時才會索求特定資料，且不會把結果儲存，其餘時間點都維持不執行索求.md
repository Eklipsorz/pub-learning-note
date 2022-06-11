Lazy loading：

  

- 相對於 Eagerly loading，Lazy 表示當需求來臨時，強調某些人事物並不會迫切地需要人事物，等到真正要處理的時候才會去做需要這動作，搭配 loading 代表著當需求來臨時，不會迫切地需要人事物的 loading，或者指當需求來臨時，並不會先去 loading 需要的內容，而是等到真正要處理的時候才會去做 loading 的動作

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

  

參考資料：

  

- [what-is-eager-loading](https://stackoverflow.com/questions/1299374/what-is-eager-loading)

- [eager-loading-and-lazy-loading](https://chuyi.inow.tw/2013/02/eager-loading-and-lazy-loading/)

## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: #📥 
Tags:
[[Databse]]
Links:
[[Database - Eager loading 是指主動索求未來會用到的資料集合並將結果放入特定空間，然後透過儲存結果來處理，以減緩不必要的處理]]
References: