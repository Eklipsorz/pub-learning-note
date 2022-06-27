## 描述

[[@wikidataACID2022]] 所描述：
> Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely or fails completely: if any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors, and crashes. A guarantee of atomicity prevents updates to the database from occurring only partially, which can cause greater problems than rejecting the whole series outright. As a consequence, the transaction cannot be observed to be in progress by another database client.

重點：
- Atomicity 是 Database Transaction 協議內容的附加執行規則之一，不過並不是所有Transaction都會有這樣子的特性，得看實際資料庫系統或開發者是否提供對應特性
- Atomicity 表示協議內容上所有要執行的任務們視為一個不可切割的原子，任何一個任務都不能獨自被完成或者任一個任務都不能夠獨自被執行失敗，最後執行結果只會有：
	- 全部要執行的任務都執行成功，並且所有任務對於資料庫的內容都一率以指定變更內容為主
	- 全部要執行的任務都執行失敗，並且所有任務對於資料庫的內容都一率還原成執行前。
- 提供Atomicity 這概念是確保避免 **任一個指派任務獨自完成且其餘任務皆為失敗所造成這兩者情況下的資料庫內容改變，這些內容改變對於協議上來說，可能衍生成嚴重的完整性和一致性問題**
> which can cause greater problems than rejecting the whole series outright


### 具體實現手段為
1. 提供語法來讓開發者制定哪些任務為協議上所要做的任務，換言之，將特定任務協議：
	- begin ：制定哪個任務定義為協議的一部分
	- commit /end：制定哪個任務做協議上的結尾以及執行到commit就自動
	- rollback：當協議上的任一任務執行失敗就回到協議的一開始，也就是begin
- transaction atomicity
![](https://docs.oracle.com/cd/E18283_01/server.112/e16508/img/cncpt025.gif)

## 複習
#🧠 Database Transaction 的 Atomicity 是指什麼？跟協議內容有何關係？ ->->-> `表示協議內容上所有要執行的任務們視為一個不可切割的原子，任何一個任務都不能獨自被完成或者任一個任務都不能夠獨自被執行失敗，最後執行結果只會有： 全部要執行的任務都執行成功，並且所有任務對於資料庫的內容都一率以指定變更內容為主、全部要執行的任務都執行失敗，並且所有任務對於資料庫的內容都一率還原成執行前。`
<!--SR:!2022-06-30,3,250-->

#🧠 Database Transaction  提出Atomicity 是為了什麼？->->-> `提供Atomicity 這概念是確保避免 **任一個指派任務獨自完成且其餘任務皆為失敗所造成這兩者情況下的資料庫內容改變，這些內容改變對於協議上來說，可能衍生成嚴重的完整性和一致性問題**`
<!--SR:!2022-06-30,3,250-->


#🧠 Database：每一個Transaction上都必定有Atomicitiy這特性嗎？ ->->-> `Atomicity 是 Database Transaction 協議內容的附加執行規則之一，不過並不是所有Transaction都會有這樣子的特性，得看實際資料庫系統或開發者是否提供對應特性`
<!--SR:!2022-06-30,3,250-->

#🧠 Database Transaction：具體上是如何實現Atomicity? (提示：制定範圍、回報、rollback) ->->-> ` 提供語法來讓開發者制定哪些任務為協議上所要做的任務，換言之，將特定任務協議： - begin ：制定哪個任務定義為協議的一部分 - commit /end：制定哪個任務做協議上的結尾以及執行到commit就自動 - rollback：當協議上的任一任務執行失敗就回到協議的一開始，也就是begin`
<!--SR:!2022-06-30,3,250-->


---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataACID2022]]