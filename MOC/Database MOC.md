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

- referential integrity
[[Database - Referential integrity 是指一筆資料紀錄上的外鍵是否都能在原本參考到表格上找到對應的紀錄之特性]]
[[Database - 若沒在資料庫系統設定外鍵的話，資料庫系統就無法保證外鍵在參考表格上能否找到對應紀錄以及無法清楚資料表格間的關係]]
[[Database - 外鍵的產生是為了讓原本資料很好地被切割以及很好地透過外鍵來將切割資料合併成原本資料]]

- data cleansing
[[data cleaning 是一種偵測資料集合中是否有髒資料並進行清洗的程序，髒資料會是指違反資料完整性、資料一致性特性的資料]]

- Database transaction
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]


### ACID

- Atomicity
[[Transaction - Atomicity 是指協議上所有被執行的任務直接都視為一個不可分割的原子，任何一個任務不能單獨被完成，只有全部任務完成或者全部任務不完成]]

- Consistency
[[Transaction - Consistency 是指只要執行協議上的指定任務之後都能產生同個結果，其結果為其資料庫都會是維持著完整性、一致性的特性]]

- Isolation
[[Transaction - Isolation 是指在資料庫上則是指每個同時被執行的協議在存取同筆紀錄時，得為了確保資料庫的一致性和完整性，要與部分協議保持隔離的狀態，讓自己能在確保資料的狀態下存取同]]

### 資料操作
- Eager Loading
[[Database - Eager loading 是指主動索求未來會用到的資料集合並將結果放入特定空間，然後透過儲存結果來處理，以減緩不必要的處理]]
[[SQL 語法中的JOIN 查詢 皆先將相關連的表格連結再一起並另外儲存，然後再從中讓集合的每個元素去從儲存結果找到相關連的紀錄]]

- Lazy Loading
[[Database - Lazy Loading 是當索求需求來臨時才會索求特定資料，且不會把結果儲存，其餘時間點都維持不執行索求]]

## 序號的唯一性
- UUID
[[UUID 是憑藉著產出的序號所給予的重疊率近為0而產出之特性的獨特序號]]


## 資料存取策略
- Read/Write Splitting
[[Read-Write Splitting 是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機]]

## ORM/ODM
- N + 1 Queries Problem
[[Database - N + 1 Queries Problem當向資料庫發送一筆Query來索要特定集合的N筆紀錄，那麼會因沒事先紀錄與特定集合相關連的集合而發送N+1筆Queries來實現]]

- ORM 何時轉換SQL語法
[[通常ORM 到真正需要資料的時候，才會替應用程式轉換對應SQL語法來向資料庫系統發送請求]]

## 前置知識
- query 是向資料庫索要特定資料的請求或者要求讀取
[[SQL 中的Query 是向資料庫索要特定資料的請求或者詢問]]

- commit 
[[CS - Commit 是指將資料上的暫行性修改轉換成資料上的永久性修改之行為]]
### Sequelize
- Sequelize 上的UUID
[[Sequelize 上的UUID 具體來說會在不同資料庫系統有著不同的資料型別]]

