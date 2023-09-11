## 描述
[[@wikidataChiJiuXing2022]]  所描述：

> **持久性**（英語：Durability）定義了資料庫系統中保證已提交的資料庫交易（transactions）將永久存在。


[[@DurabilityDatabaseSystems2021]] 所描述：
> In database systems, **durability** is the ACID property which guarantees that transactions that have committed will survive permanently.

重點：
- Durability 本意為能夠持續特定正常狀態至很長一段時間的性質，在這裡會是指協議修改後的資料庫內容會持續存在很長一段時間，意旨為當從協議的暫時性修改轉換成永久性修改，其內容將會永久存在
-  Durability 意旨為當成功執行Transaction，其資料庫的修改內容將會以Transaction指定修改的內容來永久性儲存

### 具體來說
- Durability 性質是保證協議只要執行到commit從而使資料庫內容轉換成永久性修改時，其內容將會永久存在，不會還原



### Durability 命名緣由
> the quality of being able to last a long time without becoming damaged:
> the fact of being able to continue to exist:
重點：
- Durability是指能夠維持特定狀態至很長一段時間都不受到改變的性質

## 複習
#🧠 Durability命名緣由是什麼？ ->->-> `是指能夠維持特定狀態至很長一段時間都不受到改變的性質`
<!--SR:!2023-09-30,92,228-->


#🧠  Durability 套用在Database的Transaction會是指？(從Durability命名來描述，不用實際談論Durability 在資料庫上的約束) ->->-> `Durability 本意為能夠持續特定正常狀態至很長一段時間的性質，在這裡會是指協議修改後的資料庫內容會持續存在很長一段時間，意旨為當從協議的暫時性修改轉換成永久性修改，其內容將會永久存在`
<!--SR:!2025-01-19,563,250-->

#🧠 Database： Durability 在Transaction是什麼樣的規則？修改內容會以什麼為主？ ->->-> `-  Durability 意旨為當成功執行Transaction，其資料庫的修改內容將會以Transaction指定修改的內容來永久性儲存`
<!--SR:!2023-12-30,109,210-->

#🧠 Database：若給你Commit 和Rollback的話， 會如何描述Durability 在Transaction是什麼樣的規則   ->->-> ` Durability 性質是保證協議只要執行到commit從而使資料庫內容轉換成永久性修改時，其內容將會永久存在，不會還原`
<!--SR:!2024-09-05,488,250-->




---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
[[CS - Commit 是指將資料上的暫行性修改轉換成資料上的永久性修改之行為]]
References:
[[@wikidataChiJiuXing2022]]
[[@DurabilityDatabaseSystems2021]]