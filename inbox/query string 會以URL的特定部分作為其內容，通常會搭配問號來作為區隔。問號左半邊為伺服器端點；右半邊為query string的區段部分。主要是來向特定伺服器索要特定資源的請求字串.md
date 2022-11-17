## 描述



### Query String
[[@wikidataQueryString2022]] 所描述
> A **query string** is a part of a uniform resource locator (URL) that assigns values to specified parameters

> Typical URL containing a query string is as follows:

> `https://example.com/over/there?name=ferret`

> When a server receives a request for such a page, it may run a program, passing the query string, which in this case is `name=ferret`, unchanged to the program. The question mark is used as a separator, and is not part of the query string

重點：
- query string 會以URL的特定部分作為其內容，通常會搭配特定符號來作為區隔：
	- 特定符號：通常會是問號?，問號左半邊為伺服器端點；右半邊為query string的區段部分
```
https://example.com/over/there?name=ferret
```
- 主要是來向特定伺服器索要特定資源的請求字串：伺服器接收到會以特定處理來回傳結果給予請求端
- string的組成會是由key-value pair而構成，若有多組key-value pair會搭配&來連接
```
// 一組key-value pair
key1=value1
// 多組key-value pair
key1=value1&key2=value2
```
- query string 內容本質在客戶端和伺服器之間會以百分比編碼或者URL編碼來進行
- 細節：
	- Query String 又名為 Search Parameter




## 複習


#🧠 query string 會是什麼？用途是什麼？->->-> ` query string 會以URL的特定部分作為其內容，通常會搭配特定符號來作為區隔；主要是來向特定伺服器索要特定資源的請求字串`

#🧠 query string 會是以URL的特定部分作為其內容，請問用途是什麼？ ->->-> `主要是來向特定伺服器索要特定資源的請求字串`

#🧠 query string 會是以URL的特定部分作為其內容，用途會是來向特定伺服器索要特定資源的請求字串，若伺服器接收到會是？ ->->-> `伺服器接收到會以特定處理來回傳結果給予請求端`

#🧠 query string 會以URL的特定部分作為其內容，通常會搭配特定符號來作為區隔，特定符號通常會是什麼？ 哪邊才是query string?->->-> `通常會是問號?問號左半邊為伺服器端點；右半邊為query string的區段部分`

#🧠 query string 會以URL的特定部分作為其內容，通常會搭配特定符號來作為區隔，特定符號通常會是問號，請舉例說明->->-> `https://example.com/over/there?name=ferret`

#🧠 query string本身構成是什麼結構？ ->->-> `key-value pair`

#🧠 query string本身構成是什麼結構？若有多個key-value pair ->->-> `若有多組key-value pair會搭配&來連接`

#🧠 query string在傳遞過程中會是以什麼編碼方式來編碼/解法->->-> ` query string 內容本質在客戶端和伺服器之間會以百分比編碼或者URL編碼來進行`

#🧠 Query string 別名為何？ ->->-> `Query String 又名為 Search Parameter`




---
Status: #🌱 
Tags:
[[HTML]]
Links:
[[QueryString 加號問題 - 伺服器在解析query參數時就會自動以無UTF8形式來解碼，其+被解出來會是空白]]
References: