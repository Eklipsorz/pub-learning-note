## 資料
- hot、warm、cold
[[hot、cold、warm 是強調著資料的使用率，hot是頻繁存取的資料、cold是偶爾存取的資料、warm則是之間]]

- backup type
[[hot backup 是指在備份系統與實際要備份資料的系統同時併行下進行實時備份或者頻率高到像實時的備份任務]]
[[cold backup 是指在實際備份資料的系統離線下進行備份]]
[[warm backup 是備份系統與實際要備份資料的系統同時執行下進行備份頻率介於cold和hot之間的備份]]

- lock type
[[資料庫的Shared Lock是一旦有人鎖死就只允許在鎖死期間給任何人觀看，但無人能夠修改和刪除]]
[[資料庫的Exclusive lock是一旦有人鎖死就只允許在鎖死期間給第一個鎖上的人進行讀寫存取，其他人不能參與存取]]


- database cursor
[[Database Cursor 是一個用字串或數字去對應過去處理結果並透過該索引值來將呈現資料導向成對應處理結果之機制]]
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
[[Forward-only cursor 是只紀錄使用者接下來要指向的資料集合，過去所遍歷的資料集合將會直接釋放]]

## 序號的唯一性
- UUID
[[UUID 是憑藉著產出的序號所給予的重疊率近為0而產出之特性的獨特序號]]


## 資料存取策略
- Read/Write Splitting
[[Read-Write Splitting 是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機]]

## ORM/ODM


### Sequelize
- Sequelize 上的UUID
[[Sequelize 上的UUID 具體來說會在不同資料庫系統有著不同的資料型別]]

