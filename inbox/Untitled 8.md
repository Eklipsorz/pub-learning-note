## 描述


### 瀏覽器對於URL變動的預設處理

瀏覽器對於URL變動的預設處理會是
	- 向對應端點發送請求、並搭配著符合端點的cookie也一起發送過去。


### SPA + routing 對於URL變動的處理

SPA + routing 本身來說會監聽URL變動，若變動就從客戶端的JS bundle 和 實體webpage檔案來產生對應的虛擬webpage頁面，並於瀏覽器直接呈現，在這裡，客戶端並不會為了URL而索要對應的
實體webpage頁面

#### 若要實現的話
1. 必須關閉瀏覽器對於URL變動的預設處理
2. 要有程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage。

react router provide：client-side routing
### client-side routing

> Client side routing allows your app to update the URL from a link click without making another request for another document from the server. Instead, your app can immediately render some new UI and make data requests with `fetch` to update the page with new information.

：由客戶端根據URL變動來產生對應的webpage提供畫面和服務


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: