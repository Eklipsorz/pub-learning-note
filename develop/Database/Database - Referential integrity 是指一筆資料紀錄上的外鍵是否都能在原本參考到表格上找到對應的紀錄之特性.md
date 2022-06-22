
## 描述
[[@wikidataReferentialIntegrity2021]] 所描述：

> **Referential integrity** is a property of data stating that all its references are valid.

> Some relational database management systems (RDBMS) can enforce referential integrity, normally either by deleting the foreign key rows as well to maintain integrity, or by returning an error and not performing the delete

重點：
- Referential integrity 是指資料紀錄上的外鍵屬性是否都能夠在原本參考到的表格上對應到對應紀錄 之性質：
	- 若都能對應到，代表表格間具備著Referential integrity這特性。
	- 若任一個沒對應到，代表表格間出現Link broken，這代表無法從外鍵來找到對應資料
- 通常要保證資料庫是能夠具備Referential integrity特性，得由以下角色來保證：
	- 由資料庫系統來實現，具體會是每一次對表格上的紀錄進行操作時，就檢查操作是否違反其特性，若違反就報錯並不允許執行操作
	- 由開發者自己實現，具體就是盡量不去刪掉被其他紀錄參照的紀錄，比如説表格1的紀錄1參照於表格2的紀錄2，那麼就盡量不刪掉表格的紀錄2

### 範例1：若資料庫系統沒確保Referential integrity

[[@ibmIBMDocs2021]] 所描述：

> Foreign keys join tables and establish dependencies between tables. tables can form a hierarchy of dependencies in such a way that if you change or delete a row in one table, you destroy the meaning of rows in other tables. For example, the following figure shows that the **customer_num** column of the **customer** table is a primary key for that table and a foreign key in the **orders** and **cust_call** tables. Customer number 106, George Watson™, is _referenced_ in both the **orders** and **cust_calls** tables. If customer 106 is deleted from the **customer** table, the link between the three tables and this particular customer is destroyed.

![](https://www.ibm.com/docs/en/SSGU8G_14.1.0/com.ibm.sqlt.doc/sqlt009.gif)
> When you delete a row that contains a primary key or update it with a different primary key, you destroy the meaning of any rows that contain that value as a foreign key. Referential integrity is the logical dependency of a foreign key on a primary key. The integrity of a row that contains a foreign key depends on the integrity of the row that it references—the row that contains the matching primary key.

重點：在這裡是假設三個表格-客戶表格、訂單表格、客戶通話表格
- 在這裡客戶表格的主鍵為customer_num
- 訂單表格上的customer_num 是外鍵，並用來參照於對應客戶表格上的紀錄，意旨為訂單紀錄可透過該屬性從客戶表格上找到對應紀錄
- 客戶通話表格的customer_num 是外鍵，並用參照於對應客戶表格上的紀錄，意旨為客戶通話紀錄可透過該屬性從客戶表格上找到對應紀錄
- 若客戶表格上直接移除106這筆紀錄的話：
	- 擁有106的訂單紀錄和客戶表格上的106紀錄之間發生link broken
	- 擁有106的客戶通話紀錄和客戶表格上的106紀錄之間發生link broken

### 範例2：若資料庫系統沒確保Referential integrity

[[@wikidataReferentialIntegrity2021]] 所描述：

> An example of a database that has not enforced **referential integrity**. In this example, there is a foreign key (artist_id) value in the album table that references a non-existent artist — in other words there is a foreign key value with no corresponding primary key value in the referenced table. What happened here was that there was an artist called "Aerosmith", with an artist_id of 4, which was deleted from the artist table. However, the album "Eat the Rich" referred to this artist. With referential integrity enforced, this would not have been possible.
![](https://upload.wikimedia.org/wikipedia/commons/1/13/Referential_integrity_broken.png)

重點：在這裡是假設兩個表格-作曲家表格、專輯表格
- 作曲家表格的主鍵為artist_id
- 專輯表格的每筆紀錄都有artist_id外鍵去參照於作曲家表格上的紀錄
- 若作曲家表格上的artist_id為4之紀錄被刪去，那麼專輯表格上擁有artist_id為4的紀錄將無法透過4從作曲家表格找到對應紀錄。

## 複習
#🧠 Database:  Referential integrity 是什麼？->->-> `資料紀錄上的外鍵屬性是否都能夠在原本參考到的表格上對應到對應紀錄 之性質， 若都能對應到，代表表格間具備著Referential integrity這特性，若任一個沒對應到，代表表格間出現Link broken，這代表無法從外鍵來找到對應資料`

#🧠 Database: 誰來保證資料庫上是能夠具備Referential integrity？具體來說會做什麼？ (提示：系統和使用者)->->-> `由資料庫系統來實現，具體會是每一次對表格上的紀錄進行操作時，就檢查操作是否違反其特性，若違反就報錯並不允許執行操作；由開發者自己實現，具體就是盡量不去刪掉被其他紀錄參照的紀錄，比如説表格1的紀錄1參照於表格2的紀錄2，那麼就盡量不刪掉表格的紀錄2`


	

#🧠 若資料庫系統沒確保Referential integrity，在這裡是假設三個表格-客戶表格、訂單表格、客戶通話表格，在這裡客戶表格的主鍵為customer_num，其餘兩個表格上的紀錄皆參照於客戶表格，試著解釋若刪除/變更客戶表格上的106客戶，會發生什麼情況 ？ ![](https://www.ibm.com/docs/en/SSGU8G_14.1.0/com.ibm.sqlt.doc/sqlt009.gif)->->-> `- 訂單表格上的customer_num 是外鍵，並用來參照於對應客戶表格上的紀錄，意旨為訂單紀錄可透過該屬性從客戶表格上找到對應紀錄 - 客戶通話表格的customer_num 是外鍵，並用參照於對應客戶表格上的紀錄，意旨為客戶通話紀錄可透過該屬性從客戶表格上找到對應紀錄 - 若客戶表格上直接移除106這筆紀錄的話： - 擁有106的訂單紀錄和客戶表格上的106紀錄之間發生link broken - 擁有106的客戶通話紀錄和客戶表格上的106紀錄之間發生link broken`


#🧠 若資料庫系統沒確保Referential integrity，在這裡是假設兩個表格-作曲家表格、專輯表格，專輯表格的每筆紀錄都有artist_id外鍵去參照於作曲家表格上的紀錄，那麼當刪除/變更作曲家表格上的4號作曲家，會發生什麼事情，解釋一下 ![](https://upload.wikimedia.org/wikipedia/commons/1/13/Referential_integrity_broken.png) ->->-> `- 若作曲家表格上的artist_id為4之紀錄被刪去，那麼專輯表格上擁有artist_id為4的紀錄將無法透過4從作曲家表格找到對應紀錄。`

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@wikidataReferentialIntegrity2021]]
[[@ibmIBMDocs2021]]
