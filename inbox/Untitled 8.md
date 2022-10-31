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
- dynamic URL：特定頁面/服務所對應的URL會是經過請求處理方的處理執行狀況而產生對應關係，在這裡包含了
	- 頁面/服務內容可以依據請求方給定參數而決定或者頁面/服務內容本身是固定，只是其URL的對應關係是求處理方的處理執行狀況而產生的
	- 若是SSR(Single-Side Rendering)的話，處理方會是伺服器
	- 若是CSR(Client-Side Rendering)的話，處理方會是客戶端
- 具體來說，客戶端會在URL填入特定範疇的參數來傳遞至處理方，處理方收到後就檢查URL並產生對應畫面來回傳客戶端
- 適用場景為頁面畫面或者服務是依賴著URL給定的參數來產生的


#### Static URL
[[@DynamicURLsVs]]
> A static URL is one that does not change, so it typically does not contain any URL parameters

重點：
- static URL 是指特定頁面/服務會固定對應在N個URL，其特定頁面/服務所對應的URL本身並不會依據請求處理方的處理執行狀況而改變對應關係。



## 複習


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@whatis.comWhatDynamicURL]]
[[@DynamicURLsVs]]