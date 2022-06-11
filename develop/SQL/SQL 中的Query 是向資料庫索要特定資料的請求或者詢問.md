## 描述
[[@martingibbsWhatQuerySQL]] 所描述：
> A **query** is really a question or request for data. For example, ''Tell me how many books there are on computer programming'' or ''How many Rolling Stones albums were produced before 1980?'' When we query databases, we can use a common language to get the information. **Structured Query Language SQL)**, is a fairly universal language. There are some different flavors, but once you know the basics you can easily adapt your questions.

[[@wikidataSQL2022]] 所描述：
> The scope of SQL includes data query, data manipulation (insert, update and delete), data definition ([schema](https://en.wikipedia.org/wiki/Database_schema "Database schema") creation and modification), and data access control. Although SQL is essentially a [declarative language](https://en.wikipedia.org/wiki/Declarative_programming "Declarative programming") ([4GL](https://en.wikipedia.org/wiki/4GL "4GL")), it also includes [procedural](https://en.wikipedia.org/wiki/Procedural_programming "Procedural programming") elements.


重點為：
- query 是指向資料庫索要特定資料集合的請求或者問題，通常在資料庫操作中是負責讀取操作
- 剩下非讀取的操作皆不是query

### Note
1. query 是指一個對某件事物的疑問或者向權威尋求解答的問題，在資料庫系統當中，會是指後者的意思，權威是指資料庫系統，尋求則是索要，解答則是特定資料集合，問題則是請求，合併起來就是向資料庫系統索要特定資料集合的請求或者問題
> **a question, often expressing doubt about something or looking for an answer from an authority**


## 複習
#🧠  SQL 中的Query 原意是什麼意思？(請用字典來描述 a question, often expressing doubt about something or looking for an answer from an authority )->->-> `query 是指一個對某件事物的疑問或者向權威尋求解答的問題，在資料庫系統當中，會是指後者的意思，權威是指資料庫系統，尋求則是索要，解答則是特定資料集合，問題則是請求，合併起來就是向資料庫系統索要特定資料集合的請求或者問題`

#🧠 SQL 中的Query 具體來說是什麼樣的操作？（不用按字面上原意來解釋) 那麼向資料庫做更新、新增的請求 是算Query ? ->->-> `query 是指向資料庫索要特定資料集合的請求或者問題，通常在資料庫操作中是負責讀取操作，剩下非讀取的操作皆不是query`
<!--SR:!2022-06-14,3,250-->

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@wikidataSQL2022]]
[[@martingibbsWhatQuerySQL]]