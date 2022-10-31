## 描述



### Dynamic URL

[[@whatis.comWhatDynamicURL]]
> A dynamic URL is the address - or Uniform Resource Locator ([URL](https://www.techtarget.com/searchnetworking/definition/URL)) - of a Web page with content that depends on variable parameters that are provided to the server that delivers it. The parameters may be already present in the URL itself or they may be the result of user input. A dynamic URL can often be recognized by the presence of certain characters or character strings that appear in the URL (visible in the address bar of your browser). The following are representative:

> & $ + = ? % cgi


重點：
- dynamic URL 會是專以webpage為主，而非以URL為主，故此可以稱呼為dynamic URL of a 
- dynamic URL of a webpage：特定webpage的頁面內容會是由客服端著URL給定的參數
- 
- 意旨為特定webpage所代表的頁面所對應的URL會是根據處理方處理請求時而產生
	- 若是SSR(Single-Side Rendering)的話，處理方會是伺服器
	- 若是CSR(Client-Side Rendering)的話，處理方會是客戶端
- 具體來說，客戶端會在URL填入特定範疇的參數來傳遞至處理方，處理方收到後就檢查URL並產生對應畫面來回傳客戶端
- 適用場景為頁面畫面或者服務是依賴著URL給定的參數來產生的


### Static URL

> A static URL is one that does not change, so it typically does not contain any URL parameters

重點：
- static URL 是指特定頁面/服務的

## 複習


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@whatis.comWhatDynamicURL]]