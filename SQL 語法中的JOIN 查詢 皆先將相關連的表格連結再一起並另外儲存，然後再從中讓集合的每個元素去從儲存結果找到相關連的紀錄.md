## 描述
SQL 語法中的JOIN 查詢皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄。


## 複習
#🧠 SQL 語法中的JOIN 查詢  是eager loading? 還是lazy loading?  ->->-> `是eager loading，先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到(查詢)相關連的紀錄`
<!--SR:!2022-06-14,3,250-->

---
Status: #🌱 
Tags:
[[Database]]
Links:
[[Database - N + 1 Queries Problem當向資料庫發送一筆Query來索要特定集合的N筆紀錄，那麼會因沒事先紀錄與特定集合相關連的集合而發送N+1筆Queries來實現]]
[[Database - Eager loading 是指主動索求未來會用到的資料集合並將結果放入特定空間，然後透過儲存結果來處理，以減緩不必要的處理]]
References: