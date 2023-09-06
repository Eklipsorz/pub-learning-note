## 描述

### Dynamic URL vs. Static URL

在這裡的URL都泛指著特定頁面/服務所會對應的URL，其URL對應關係是否會依據著請求處理方的處理執行狀況而產生對應關係，而分成：
- Dynamic URL
- Static URL

#### Dynamic URL

[[@whatis.comWhatDynamicURL]]
> A dynamic URL is the address - or Uniform Resource Locator ([URL](https://www.techtarget.com/searchnetworking/definition/URL)) - of a Web page with content that depends on variable parameters that are provided to the server that delivers it. The parameters may be already present in the URL itself or they may be the result of user input. A dynamic URL can often be recognized by the presence of certain characters or character strings that appear in the URL (visible in the address bar of your browser). The following are representative:

> & $ + = ? % cgi


重點：
- dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係
	- 若是SSR(Single-Side Rendering)的話，處理方會是伺服器
	- 若是CSR(Client-Side Rendering)的話，處理方會是客戶端
	- 若只有處理用的參數，卻沒處理方的處理，就不會對應到原本要處理才能得到的頁面/服務
- 在這裡包含了
	- 頁面/服務內容會依據請求方給定參數而決定
	- 頁面/服務內容本身是並不會依據請求方給定參數決定，只是其URL的對應關係是求處理方的處理執行狀況而產生的


##### Dynamic URL 請求處理方的參數是

參數：
- 具體來說，客戶端會在URL填入特定參數來傳遞至處理方，處理方收到後就檢查URL並作為參數來處理，接著處理方就根據處理結果來對應特定頁面/服務
- 若以URL的一部分作為參數的話，其參數會是URL parameters 或者稱之為params


#### Static URL
[[@DynamicURLsVs]]
> A static URL is one that does not change, so it typically does not contain any URL parameters

重點：
- static URL：是指特定頁面/服務和URL的對應關係不透過請求處理執行時來決定，而是在執行前就決定好，且URL本身並不會依據請求處理方的處理執行狀況而改變對應關係。




## 複習

#🧠 URL 本身是指特定頁面/服務所對應的URL，其對應關係可以依據什麼而分成Dynamic URL或者Static URL ->->-> `是否會依據著請求處理方的處理執行狀況而產生對應關係`
<!--SR:!2024-01-04,261,248-->

#🧠 dynamic URL 是什麼？ ->->-> `特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係`
<!--SR:!2024-01-12,267,248-->

#🧠 static URL 是什麼？ ->->-> `是指特定頁面/服務和URL的對應關係不透過請求處理執行時來決定，而是在執行前就決定好，且URL本身並不會依據請求處理方的處理執行狀況而改變對應關係。`
<!--SR:!2024-01-13,263,248-->

#🧠 若特定頁面/服務和URL之間的對應關係是static URL，那麼會不會因為請求處理方的執行而改變？  ->->-> `不會`
<!--SR:!2023-11-30,236,248-->

#🧠 若特定頁面/服務和URL之間的對應關係是dynamic URL，那麼會不會因為請求處理方的執行而改變？  ->->-> `有可能`
<!--SR:!2023-11-05,221,248-->


#🧠 dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，若沒有處理方的處理，只有處理用的參數，請問還能對應到原本要處理才能得到的頁面/服務嗎？為什麼？ ->->-> `並不能，主要是dynamic URL的對應關係就是得經過處理方處理才能達成，所以並不能到原本要處理才能得到的頁面/服務`
<!--SR:!2025-01-19,500,250-->

#🧠 dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，請問這裡處理方在SSR和CSR各是什麼 ->->-> `若是SSR(Single-Side Rendering)的話，處理方會是伺服器。若是CSR(Client-Side Rendering)的話，處理方會是客戶端`
<!--SR:!2023-10-25,216,248-->

#🧠 dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，請問頁面和請求方給定參數之間會包含什麼情況？ ->->-> `	- 頁面/服務內容會依據請求方給定參數而決定 - 頁面/服務內容本身是並不會依據請求方給定參數決定，只是其URL的對應關係是求處理方的處理執行狀況而產生的`
<!--SR:!2024-02-19,284,248-->

#🧠 dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，會用什麼當作參數？具體會是什麼？ ->->-> ` 具體來說，客戶端會在URL填入特定參數來傳遞至處理方，處理方收到後就檢查URL並作為參數來處理，接著處理方就根據處理結果來對應特定頁面/服務`
<!--SR:!2023-12-15,246,248-->


#🧠 dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，若以URL的一部分作為參數的話，其參數會是叫什麼？ ->->-> `URL parameters 或者稱之為params`
<!--SR:!2023-11-27,146,210-->



---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@whatis.comWhatDynamicURL]]
[[@DynamicURLsVs]]