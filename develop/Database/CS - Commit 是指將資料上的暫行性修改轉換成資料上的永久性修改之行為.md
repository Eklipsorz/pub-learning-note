

## 描述
[[@wikidataCommitDataManagement2021]] 所描述的
> In computer science and data management, a **commit** is the making of a set of tentative changes permanent, marking the end of a transaction and providing _Durability_ to ACID transactions. A _commit_ is an act of committing.

重點：
- 在電腦科學裡，commit是指將資料上的暫時性修改轉換成永久性修改的行為
- 在資料庫或者資料管理，資料庫會是運用在transaction上，並主要負責：
	- 使資料庫系統將transaction所做的資料庫內容上暫時性修改轉換資料庫內容上永久性修改
	- 告知資料庫系統該transaction已經結束了

## 複習
#🧠 在電腦科學裡，commit 是指什麼樣的動作 (提示：資料)->->-> `commit是指將資料上的暫時性修改轉換成永久性修改的行為`

#🧠 commit 運用在資料庫上的transaction的話，會是負責什麼？(協議如何告知結束、如何修改資料庫)->->-> `使資料庫系統將transaction所做的資料庫內容上暫時性修改轉換資料庫內容上永久性修改、告知資料庫系統該transaction已經結束了`

---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Transaction - Atomicity 是指協議上所有被執行的任務直接都視為一個不可分割的原子，任何一個任務不能單獨被完成，只有全部任務完成或者全部任務不完成]]
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataCommitDataManagement2021]]