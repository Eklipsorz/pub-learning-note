

## 描述

[[@wikidataACID2022]] 所描述：
> **Isolation**
> 
> Transactions are often executed concurrently (e.g., multiple transactions reading and writing to a table at the same time). Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially. Isolation is the main goal of concurrency control; depending on the method used, the effects of an incomplete transaction might not even be visible to other transactions.

重點：
-  Transaction 時常同時被執行，換言之，會有個多個transaction同時在向表格讀取和寫入資料至表格內，通常只要多個transaction同時存取同個資料集合就會出錯，因此而提出isolation規則
- Isolation 是指在資料庫上則是指每個同時被執行的協議在存取同筆紀錄時，得為了確保資料庫的一致性和完整性，要與部分協議保持隔離的狀態，讓自己能在確保資料的狀態下存取同樣紀錄，而其餘想存取紀錄的協議得等待，就如同將多個同時執行的協議轉換成序列式執行(同時只能有一個協議能夠存取重複紀錄)
- Isolation 是為了避免多個同時執行的Transaction在同筆紀錄上發生資料上的不一致、不完整
- Isolation 會是 concurrency control的目標

### Isolation 命名緣由

> the state of being alone or lonely
重點：
- Isolation 是指某東西A與什麼保持距離以維持自己被隔離、孤立的狀態
- 形容在資料庫上則是指每個同時被執行的協議在存取同筆紀錄時，得為了確保資料庫的一致性和完整性，要與部分協議保持隔離的狀態，讓自己能在同期間存取同樣紀錄
## 複習
#🧠 Isolation 命名緣由為何？ (與xx保持距離) ->->-> `Isolation 是指某東西A與什麼保持距離以維持自己被隔離、孤立的狀態`
<!--SR:!2024-07-27,430,230-->

#🧠 為何要提出isolation 這概念 ？請從多個transaction同時執行來說起，並以結果是否被影響以及是否不如預期做為結尾？->->-> ` Transaction 時常同時被執行，換言之，會有個多個transaction同時在向表格讀取和寫入資料至表格內，通常只要多個transaction同時存取同個資料集合就會發生不一致、完整性問題，進而衍生出多個transaction相互影響他們各自的執行結果，使結果不如預期，因此而提出isolation規則`
<!--SR:!2024-01-12,126,228-->

#🧠  Database: Isolation 套用在每個Transaction 上會是指什麼？ (誰要被隔離？如何隔離？何時隔離) ->->-> `是指在資料庫上則是指每個同時被執行的協議在存取同筆紀錄時，得為了確保資料庫的一致性和完整性，要與部分協議保持隔離的狀態，讓自己能在同期間存取同樣紀錄，而其餘想存取紀錄的協議得等待`
<!--SR:!2023-10-20,106,230-->

#🧠 Database: Isolation 套用在每個Transaction 的話，會使執行情況會變成如何？ (序列? 並行) ->->-> `在存取同個紀錄時，每個transaction會如同排隊一般或者序列式執行，等待著部分先搶到存取權的transaction執行完畢`
<!--SR:!2025-01-16,560,250-->


#🧠 Isolation 概念在Transaction被提出是為了什麼原因？ ->->-> `Isolation 是為了避免多個同時執行的Transaction在同筆紀錄上發生資料上的不一致、不完整`
<!--SR:!2023-12-31,334,250-->


---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataACID2022]]