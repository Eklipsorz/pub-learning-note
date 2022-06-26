## 描述

[[@wikidataACID2022]] 所描述：
> Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely or fails completely: if any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors, and crashes. A guarantee of atomicity prevents updates to the database from occurring only partially, which can cause greater problems than rejecting the whole series outright. As a consequence, the transaction cannot be observed to be in progress by another database client.

重點：
- Atomicity 是 Database Transaction 協議內容的附加執行規則之一，不過並不是所有Transaction都會有這樣子的特性，得看實際資料庫系統或開發者是否提供對應特性
- Atomicity 表示協議內容上所有要執行的任務們視為一個不可切割的原子，任何一個任務都不能獨自被完成或者任一個任務都不能夠獨自被執行失敗，最後執行結果只會有：
	- 全部要執行的任務都執行成功，並且所有任務對於資料庫的內容都一率以指定變更內容為主
	- 全部要執行的任務都執行失敗，並且所有任務對於資料庫的內容都一率還原成執行前。
- 提供Atomicity 這概念是為了確保協議內容上的任一個務獨自完成可能會導致後續
> which can cause greater problems than rejecting the whole series outright
## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataACID2022]]