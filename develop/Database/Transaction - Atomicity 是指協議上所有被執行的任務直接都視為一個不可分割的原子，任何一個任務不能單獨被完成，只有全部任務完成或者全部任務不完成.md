## 描述

[[@wikidataACID2022]] 所描述：
> Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely or fails completely: if any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors, and crashes. A guarantee of atomicity prevents updates to the database from occurring only partially, which can cause greater problems than rejecting the whole series outright. As a consequence, the transaction cannot be observed to be in progress by another database client.

重點：
- Atomicity 是 Database Transaction 協議內容的附加執行規則之一，不過並不是所有Transaction都會有這樣子的特性，得看實際資料庫系統或開發者是否提供對應特性
- Atomicity 表示協議內容上所有要執行的任務們視為一個不可切割的原子，任何一個任務都不能獨自被完成或者任一個任務都不能夠獨自被執行失敗，最後執行結果只會有：
	- 全部要執行的任務都執行成功，並且所有任務對於資料庫的內容都一率以指定變更內容為主
	- 全部要執行的任務都執行失敗，並且所有任務對於資料庫的內容都一率還原成執行前。
- 提供Atomicity 這概念是確保避免 **任一個指派任務獨自完成且其餘任務皆為失敗所造成這兩者情況下的資料庫內容改變，這些內容改變對於協議上來說，可能衍生成嚴重的完整性、一致性、冗余問題**
> which can cause greater problems than rejecting the whole series outright


### 具體實現手段為
1. 提供語法來讓開發者制定哪些任務為協議上所要做的任務並且將資料變更分為暫時性修改(可被還原的修改)和永久性修改(不可被還原修改)，從begin至commit之前的資料庫變更都是暫時的，可以被撤銷的，除了執行到commit就會轉換成永久性修改並結束transaction。
	- begin ：定義協議從何開始
	- commit /end：定義協議上的結尾以及執行到commit就自動轉換永久性修改
	[[CS - Commit 是指將資料上的暫行性修改轉換成資料上的永久性修改之行為]]
	- rollback：當協議執行失敗時所會執行的操作，該操作會將目前暫時性修改撤銷，如同從未執行過transaction，另外會不會從協議開頭執行，一切都看系統支援，若不支援就跳出整個協議，若支援就從協議開頭執行
	[[Database - rollback 是指反轉特定操作執行的結果，即為將結果還原成未執行特定操作的狀態]]
- transaction atomicity
![](https://docs.oracle.com/cd/E18283_01/server.112/e16508/img/cncpt025.gif)

## 複習
#🧠 Database Transaction 的 Atomicity 是指什麼？跟協議內容有何關係？ ->->-> `表示協議內容上所有要執行的任務們視為一個不可切割的原子，任何一個任務都不能獨自被完成或者任一個任務都不能夠獨自被執行失敗，最後執行結果只會有： 全部要執行的任務都執行成功，並且所有任務對於資料庫的內容都一率以指定變更內容為主、全部要執行的任務都執行失敗，並且所有任務對於資料庫的內容都一率還原成執行前。`
<!--SR:!2024-02-20,364,250-->


#🧠 Atomicity 施加在 Database Transaction 的話，若協議部分任務執行失敗的話，資料庫結果會是如何？  協議會重新執行嗎？ ->->-> `其內容會還原成未執行整個transaction前的資料庫內容，並依據開發者或者系統是否允許重新執行transaction或者跳出整個transaction`
<!--SR:!2023-03-23,165,250-->


#🧠 Atomicity 施加在 Database Transaction 的話，若協議只有部分任務執行成功的話，資料庫結果會是如何？  協議會重新執行嗎？ ->->-> `其內容會還原成未執行整個transaction前的資料庫內容，並依據開發者或者系統是否允許重新執行transaction或者跳出整個transaction`
<!--SR:!2023-04-10,177,250-->

#🧠 Atomicity 施加在 Database Transaction 的話，若協議全部執行成功的話，資料庫結果會是如何？  協議會重新執行嗎？ ->->-> `資料庫內容會變更成執行完協議後的內容，且並不會重新執行`
<!--SR:!2023-04-02,172,250-->

#🧠 Database Transaction  提出Atomicity 是為了什麼？->->-> `提供Atomicity 這概念是確保避免 **任一個指派任務獨自完成且其餘任務皆為失敗所造成這兩者情況下的資料庫內容改變，這些內容改變對於協議上來說，可能衍生成嚴重的完整性、一致性、冗余問題**`
<!--SR:!2024-03-02,369,250-->


#🧠 Database：每一個Transaction上都必定有Atomicitiy這特性嗎？ ->->-> `Atomicity 是 Database Transaction 協議內容的附加執行規則之一，不過並不是所有Transaction都會有這樣子的特性，得看實際資料庫系統或開發者是否提供對應特性`
<!--SR:!2023-03-27,168,250-->

#🧠 Database Transaction：具體上是如何實現Atomicity? (提示：制定修改種類、制定範圍、回報、rollback) ->->-> `首先會制定修改種類：(可被還原的修改)暫時性修改、(不可被還原的修改)永久性修改，並且以begin、commit作為一個協議的範圍，當系統執行到begin，就即為執行協議，此時還未到達commit的資料庫修改都算是暫時性修改，當執行失敗時，就執行rollback，所有暫時性修改立刻被撤銷，並且跳出協議或者從頭執行，若都沒失敗一直執行到commit時，所有暫時性修改就會轉換為永久性修改，並宣布結束協議`
<!--SR:!2023-04-30,191,250-->

#🧠 Database Transaction具體上是如何實現Atomicity：進入transaction時，修改種類分為哪兩類 ->->-> `暫時性修改、永久性修改`
<!--SR:!2023-05-01,192,250-->


#🧠 Database Transaction具體上是如何實現Atomicity：進入transaction時的暫時性修改是指？ 何時觸發->->-> `暫時性修改是指可被還原的修改，換言之，會事先儲存修改前的狀態，並根據修改狀況來還原，觸發時間為從進入協議就會觸發`
<!--SR:!2023-03-12,63,230-->


#🧠 Database Transaction具體上是如何實現Atomicity：進入transaction時的永久性修改是指？ 何時觸發？->->-> `永久性修改是指不可被還原的修改，換言之，不會有事先儲存修改前的狀態來還原，觸發時間為執行到commit就轉換`
<!--SR:!2023-05-03,194,250-->

#🧠 Database Transaction：當transaction 執行到rollback 會是指什麼？是否會從協議開頭重新執行？ ->->-> `所有暫時性修改將會被撤銷，並且根據系統是否允許從協議開頭執行來進行，若沒允許就跳出協議，若允許就從協議開頭執行。`
<!--SR:!2023-10-24,293,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
[[Database - rollback 是指反轉特定操作執行的結果，即為將結果還原成未執行特定操作的狀態]]
[[CS - Commit 是指將資料上的暫行性修改轉換成資料上的永久性修改之行為]]
References:
[[@wikidataACID2022]]