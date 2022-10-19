## 描述


### Database transaction

從命名緣由可以得知transaction原意為
> 特定對象A和特定對象B要提供特定服務所要滿足的完整協議，其協議內容為所要完成的業務部分

在資料庫系統：
- 資料庫系統要替特定對象A提供特定資料的存取所要滿足的完整協議，其協議內容會以一些資料庫系統所需要執行的代碼以及附加執行規則：
	- 通常每個transaction 都會有原子性這項執行規則，部分資料庫系統上的transaction可能會擁有原子性、一致性、隔離性、永續性，但不一定全都有，全都由開發者和系統來做決定
- transaction 範例(含資料庫系統所需要執行的代碼以及原子性這項規則)
![](https://docs.oracle.com/cd/E18283_01/server.112/e16508/img/cncpt025.gif)

### transaction 命名緣由
[[@cambridgedictionaryTransactionTranslationTraditional]] 所描述：
>  a piece of business that is done between people, especially an act of buying or selling

[[@jameschenWhatTransaction]] 所描述：
> A transaction is a completed agreement between a buyer and a seller to exchange goods, services, or financial assets in return for money.

重點：
- 第一個部分：是指是指人與人之間所要完成的業務部分，尤其指購買或者販賣
- 第二個部分：是指買家和賣家之間要販售特定商品、服務、資產所要滿足的完整協議
- 兩者統整起來的話，就是特定對象A和特定對象B之間要提供特定服務所要滿足的完整協議，其協議內容為所要完成的業務部分
## 複習
#🧠 transaction 原意命名緣由為何？ (提示：協議和內容) ->->-> `特定對象A和特定對象B之間要提供特定服務所要滿足的完整協議，其協議內容為所要完成的業務部分`
<!--SR:!2023-04-24,188,250-->

#🧠 transaction 原意放在資料庫上的話，又會是什麼意思呢？ ->->-> `資料庫系統要替特定對象A提供特定資料的存取所要滿足的完整協議，其協議內容會以一些資料庫系統所需要執行的代碼以及附加執行規則，通常每個transaction 都會有原子性這項執行規則，部分資料庫系統上的transaction可能會擁有原子性、一致性、隔離性、永續性，但不一定全都有，全都由開發者和系統來做決定`
<!--SR:!2023-05-01,194,250-->


---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
References:
[[@jameschenWhatTransaction]]
[[@cambridgedictionaryTransactionTranslationTraditional]]
