## 描述



[[@mdnURLSearchParamsWebAPIs]]
> new URLSearchParams()
> The `**URLSearchParams**` interface defines utility methods to work with the query string of a URL.

重點：
- 一個內建於瀏覽器並以JS而撰寫的介面
- 該介面是專門協助開發者處理特定URL上的query string
	- 流程：
		1. 先找到其URL的query string部分
		2. 擷取query string
		3. 將query string按照key-value pair來轉換成對應物件來讓該介面很好操作
- 具體含有屬性和數個方法來操作攔截到的query string
	- 建構式：
		- options 會是指要轉換的query string
		```
		new URLSearchParams(options)
	   ```
	- URLSearchParams.get()：
		- name：要擷取的參數名稱
		```
	  URLSearchParams.get(name)
	   ```

## 複習


#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags: 
[[HTML]] - [[JavaScript]]
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
References:
[[@mdnURLSearchParamsWebAPIs]]