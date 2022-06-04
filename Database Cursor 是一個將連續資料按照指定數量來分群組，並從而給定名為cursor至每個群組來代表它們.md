
## 描述
引用[[@ibmDatabaseCursorIBM]]所描述的Database cursor：
> A database cursor is an identifier associated with a group of rows. It is, in a sense, a pointer to the current row in a buffer.

> You must use a cursor in the following cases: 

> -   Statements that return more than one row of data from the database server:
	>    -   A SELECT statement requires a select cursor.
	>    -   An EXECUTE FUNCTION statement requires a function cursor.

重點：
- cursor 原意為一個小型標記，能夠在電腦螢幕上滑動並呈現它在螢幕上的所在
> a small mark on a computer screen that can be moved and that shows the position on the screen where, for example, text will be added

- 套用在電腦科學上的資料庫，cursor則是意旨為某個資料庫上的資料集合之索引值或者識別值，換言之，cursor會是指向代表著特定資料集合，而資料集合會由多個紀錄或者多筆資料所構成
- 具體來說，會將連續資料按照指定數量來切分成好幾組資料集合，每個資料集合都會拿到cursor，當要存取特定集合上的資料，只需要指定cursor就能獲取對應集合資料
- cursor本身會是以數字來表示，而數字的制定方式則分為
	- 事先定義好的靜態指標 的 Static Cursor
	- 動態依據資料的狀況來制定 的 Dynamic Cursor
	- 每個集合上所拿到的Cursor不一定是連續性的數字。



## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@ibmDatabaseCursorIBM]]
[[@wikidataZhiBiaoZiLiaoKuWeiJiBaiKe]]
