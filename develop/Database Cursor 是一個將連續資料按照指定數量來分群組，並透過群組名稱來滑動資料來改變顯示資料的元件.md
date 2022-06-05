
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

- 套用在電腦科學上的資料庫，就是用滑動資料來改變顯示資料的元件，換言之，將原資料按照指定數量來分成好幾個群組，並給予cursor編號，來方便透過編號進行上下左右的移動來改變實際會顯示的資料
- 具體來說，會將連續資料按照指定數量來切分成好幾組資料集合，每個資料集合都會拿到cursor，當要存取特定集合上的資料，只需要指定cursor就能獲取對應集合資料
- cursor本身會是以數字來表示，而數字的制定方式則分為
	- 事先定義好的靜態指標 的 Static Cursor
	- 動態依據資料的狀況來制定 的 Dynamic Cursor
	- 每個集合上所拿到的Cursor不一定是連續性的數字。

### 用途
主要是透過cursor編號的給定，來針對特定資料做一些修改和存取

### 舉例
假設使用特定語法來獲取下圖左半邊的資料，若使用database cursor跟特定數字3的話，就會將結果資料按照3個資料來將原資料分成4個集合，同時每個集合會綁定cursor來代表自己，比如指定cursor 4就是存取對應的集合 
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654340797/blog/database/database%20cursor/database-cursor-diagram_txvrxc.png)


## 複習
#🧠  cursor 原意為何？ ->->-> `能夠在電腦螢幕上滑動並呈現它在螢幕上的所在，換言之，就是透過滑動來改變螢幕畫面(如實時更新標記在螢幕上的位置)的標記`
<!--SR:!2022-06-08,3,250-->

#🧠 cursor 原意套用在電腦科學上的資料庫會是指？->->-> `套用在電腦科學上的資料庫，就是用滑動資料來改變顯示資料的元件，換言之，將原資料按照指定數量來分成好幾個群組，並給予cursor編號，來方便透過編號進行上下左右的移動來改變實際會顯示的資料`
<!--SR:!2022-06-06,1,230-->

#🧠 database cursor 會是以什麼型別作為每個群組的識別字 ->->-> `數字`
<!--SR:!2022-06-08,3,250-->

#🧠 database cursor 用途為何->->-> `主要是透過cursor編號的給定，來針對特定資料做一些修改和存取`
<!--SR:!2022-06-08,3,250-->

#🧠 database cursor以數字來給定的話，那麼數字的給定方式會是哪些(提示:static和dynamic)->->-> `事先定義好的靜態指標 的 Static Cursor、動態依據資料的狀況來制定 的 Dynamic Cursor`
<!--SR:!2022-06-08,3,250-->


#🧠 database cursor以數字來給定的話，那麼數字的給定方式面對以下圖的右邊，其cursor1至cursor4這四個數字會是連續性數字嗎![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654340797/blog/database/database%20cursor/database-cursor-diagram_txvrxc.png)->->->`不一定`
<!--SR:!2022-06-08,3,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[Redis]] - [[Database Cursor]]
Links:
[[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]
References:
[[@ibmDatabaseCursorIBM]]
[[@wikidataZhiBiaoZiLiaoKuWeiJiBaiKe]]
