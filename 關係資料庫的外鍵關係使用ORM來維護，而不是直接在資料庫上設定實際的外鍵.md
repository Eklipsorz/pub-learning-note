


## 描述


sequelize 允許加入無法對應對應其他相關連的資料之外鍵的紀錄，比如說

庫存表格上有id、productId、price、quantity、restQuantity、createdAt、updatedAt，而productId是外鍵，會對應著產品表格上的主鍵，而sequelize允許紀錄上的外鍵是可以在產品表格對應不到任何產品。

https://island.postgresql.tw/2018/03/03/9-reasons-why-there-are-no-foreign-keys-in-your-database-referential-integrity-checks.html
## 複習


---
Status: #🌱 
Tags:
[[Database]] - [[sequelize]]
Links:
References: