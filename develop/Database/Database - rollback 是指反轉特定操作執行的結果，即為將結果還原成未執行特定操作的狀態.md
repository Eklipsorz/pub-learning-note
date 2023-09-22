

## 描述
[[@wikidataRollbackDataManagement2022]] 所描述的
> In database technologies, a **rollback** is an operation which returns the database to some previous state. Rollbacks are important for database integrity, because they mean that the database can be restored to a clean copy even after erroneous operations are performed

重點：
- 在資料庫技術中，rollback是指一種操作，能夠將目前資料庫內容返回至先前指定版本下的內容
- 通常運用在資料庫上的transaction或者特定操作，用以在transaction的某個任務出錯時或者特定操作出錯時所做出的資料庫內容修正返回至執行任務前或者執行特定操作之前的內容

### rollback 命名緣由

> the act of reducing or reversing (= changing to what it was before) the effect of a particular arrangement:

arrangement 
> a plan for how something will happen
重點：
- roll 是指滾動、轉動，back是往後，結合再一起就是為反轉
- rollback 是指反轉特定安排(一個定義某事物如何發生的計畫)的執行效果，衍生成將結果還原成執行特定安排前的狀態

## 複習
#🧠 rollback 命名緣由是什麼？ ->->-> ` roll 是指滾動、轉動，back是往後，結合再一起就是為反轉，rollback 是指反轉特定安排(一個定義某事物如何發生的計畫)的執行效果，衍生成將結果還原成執行特定安排前的狀態`
<!--SR:!2023-12-30,283,230-->

#🧠 arrangement 是什麼？->->-> `一個定義某事物如何發生的計畫`
<!--SR:!2023-10-16,199,226-->


#🧠 rollback  在資料庫中會是指什麼？(不談transaction) ->->-> `ollback是指一種操作，能夠將目前資料庫內容返回至先前指定版本下的內容`
<!--SR:!2024-09-20,442,230-->

#🧠 rollback 在資料庫上的應用是什麼？transaction? 特定操作？ ->->-> `通常運用在資料庫上的transaction或者特定操作，用以在transaction的某個任務出錯時或者特定操作出錯時所做出的資料庫內容修正返回至執行任務前或者執行特定操作之前的內容`
<!--SR:!2025-08-02,680,250-->


---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataRollbackDataManagement2022]]