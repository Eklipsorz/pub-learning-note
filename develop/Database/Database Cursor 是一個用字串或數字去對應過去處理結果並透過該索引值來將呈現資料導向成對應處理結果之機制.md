
## 描述
引用[[@ibmDatabaseCursorIBM]]所描述的Database cursor：
> A database cursor is an identifier associated with a group of rows. It is, in a sense, a pointer to the current row in a buffer.

> You must use a cursor in the following cases: 

> -   Statements that return more than one row of data from the database server:
	>    -   A SELECT statement requires a select cursor.
	>    -   An EXECUTE FUNCTION statement requires a function cursor.

重點：
- cursor 原意為一個小型標記，能夠在電腦螢幕上滑動並呈現它在螢幕上的所在，換言之，就是透過滑動來改變螢幕畫面(如實時更新標記在螢幕上的位置)的標記
> a small mark on a computer screen that can be moved and that shows the position on the screen where, for example, text will be added

- 套用在電腦科學上的資料庫，透過滑動來改變呈現的資料，滑動是指透過指定index來導向對應的資料集合

- 具體來說會做以下事情：
	- 會利用cursor字串/數字來紀錄過去所處理過的結果，透過cursor字串/數字來導向對應的資料集合，以此實現透過字串/數字滑動來改變呈現的資料是什麼。
	- 原任務A會切分成多個子任務，每個子任務所回傳的資料集合會以cursor數字來綁定，然後由多個資料集合組合成任務A單獨執行後的結果，但為了保證結果不被人修改會添加shared lock，隨後可以透過cursor字串/數字來導向對應處理結果

- cursor本身會是以數字來表示，而數字的制定方式則分為
	- 事先定義好的靜態指標 的 Static Cursor
	- 動態依據資料的狀況來制定 的 Dynamic Cursor
	- 每個集合上所拿到的Cursor不一定是連續性的數字。

### 用途
1. 透過cursor字串/數字的給定，來紀錄過去查詢結果或者處理結果，以節省未來重複做的成本
2. 呈現結果上實現分頁化


![](https://www.researchgate.net/profile/Shi-Huang-5/publication/220095117/figure/fig2/AS:670705469386752@1536920053039/Database-navigation-emulated-by-cursors.png)

### 缺點
1. 記憶體成本會隨著索引越多而增加：由於會使用字串/數字來紀錄對應的資料處理結果，所以基本上會儲存字串/數字和結果
2. 由於Database cursor會使用shared lock，會造成死結


### 舉例
假設使用特定語法來獲取下圖左半邊的資料，若使用database cursor跟特定數字3的話，就會將結果資料按照3個資料來將原資料分成4個集合，同時每個集合會綁定cursor來代表自己，比如指定cursor 4就是存取對應的集合 
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654340797/blog/database/database%20cursor/database-cursor-diagram_txvrxc.png)


## 複習
#🧠  cursor 原意為何？ ->->-> `能夠在電腦螢幕上滑動並呈現它在螢幕上的所在，換言之，就是透過滑動來改變螢幕畫面(如實時更新標記在螢幕上的位置)的標記`
<!--SR:!2022-09-20,67,250-->

#🧠 cursor 原意套用在電腦科學上的資料庫會是指？->->-> `套用在電腦科學上的資料庫，透過滑動來改變呈現的資料，滑動是指透過指定index來導向對應的資料集合`
<!--SR:!2022-09-29,74,250-->

#🧠 database cursor是什麼->->-> `Database Cursor 是一個用數字索引值去對應過去處理結果並透過該索引值來將呈現資料導向成對應處理結果之機制`
<!--SR:!2022-09-26,71,250-->

#🧠 database cursor 會是以什麼型別作為每個群組的識別字 ->->-> `字串/數字`
<!--SR:!2022-09-05,57,250-->

#🧠 database cursor 可以用來做些什麼應用(基本目的和任務切分) ->->-> `會利用cursor數字來紀錄過去所處理過的結果，透過cursor數字來導向對應的資料集合，以此實現透過數字滑動來改變呈現的資料是什麼。、原任務A會切分成多個子任務，每個子任務所回傳的資料集合會以cursor數字來綁定，然後由多個資料集合組合成任務A單獨執行後的結果，但為了保證結果不被人修改會添加shared lock，隨後可以透過cursor數字來導向對應處理結果`
<!--SR:!2022-09-29,74,250-->

#🧠 database cursor 用途為何(提示：用數字來滑動以及頁)->->-> `主要是透過cursor編號的給定，來紀錄過去查詢結果或者處理結果，以節省未來重複做的成本、實現呈現結果上實現分頁化`
<!--SR:!2022-10-17,76,230-->

#🧠 database cursor 缺點為何 (提示：記憶體和lock) ->->-> `1. 記憶體成本會隨著索引越多而增加：由於會使用數字索引值來紀錄對應的資料處理結果，所以基本上會儲存數字索引值和結果 2. 由於Database cursor會使用shared lock，會造成死結`
<!--SR:!2022-09-28,73,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[Redis]] - [[Database Cursor]]
Links:
[[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
References:
[[@ibmDatabaseCursorIBM]]
[[@wikidataZhiBiaoZiLiaoKuWeiJiBaiKe]]
