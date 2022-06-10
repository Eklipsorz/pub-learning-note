
## 描述
[[@ZhiBiaoZiLiaoKu2021]]

1. 只針對目前要移動到的cursor和對應的資料集合來紀錄和進行Shared Lock
2. 過去曾走過的cursor和對應的資料集合會直接釋放不紀錄

## 複習
#🧠 Forward-only cursor 是什麼樣的cursor機制？->->-> `只針對目前要移動到的cursor和對應的資料集合來紀錄和進行Shared Lock，過去曾走過的cursor和對應的資料集合會直接釋放不紀錄`
<!--SR:!2022-06-19,9,250-->

---
Status: #🌱 
Tags:
[[Databse]] - [[Redis]]
Links:
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
[[Database Cursor 是一個用字串或數字去對應過去處理結果並透過該索引值來將呈現資料導向成對應處理結果之機制]]
References:
[[@ZhiBiaoZiLiaoKu2021]]