## 描述


### 瀏覽器對於URL變動的預設處理

瀏覽器對於URL變動的預設處理會是
	- 向對應端點發送請求、並搭配著符合端點的cookie也一起發送過去。


### SPA + routing 對於URL變動的處理

SPA + routing 本身來說會監聽URL變動，若變動就從客戶端的JS bundle 和 實體webpage檔案來產生對應的虛擬webpage頁面，並於瀏覽器直接呈現，在這裡，客戶端並不會為了URL而索要對應的
實體webpage頁面

#### 若要親自實現的話
1. 必須關閉瀏覽器對於URL變動的預設處理
3. 要有程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage。


#### 若要以能提供routing功能的套件

具體套件為react-router：
- 實現client-side routing 的第三方套件
- 安裝方式：
	- 其中react-router本身分為react-router和react-router-dom，後者是專門提供routing功能給支援DOM介面的react app 
```
npm install react-router-dom
```




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務；server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務]]
References:
[[@reactrouterFeatureOverviewV6]]