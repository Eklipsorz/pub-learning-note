## 描述


### 瀏覽器對於URL變動的預設處理

瀏覽器對於URL變動的預設處理會是
	- 向對應端點發送新的請求來索求新網頁


### SPA + routing 對於URL變動的處理

SPA + routing 本身來說會監聽URL變動，若變動就從客戶端的JS bundle 和 實體webpage檔案來產生對應的虛擬webpage頁面，並於瀏覽器直接呈現，在這裡，客戶端並不會為了URL而索要對應的實體webpage頁面

#### 若要親自實現的話
1. 必須關閉瀏覽器對於URL變動的預設處理
2. 要有程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage。


#### 若要以能提供routing功能的套件

具體套件為react-router：
- 實現client-side routing 的第三方套件
- 安裝方式：
	- 其中react-router本身分為react-router和react-router-dom，前者是負責提供router的核心功能，後者是基於前者的基礎來向DOM渲染介面提供對應router的功能
```
npm install react-router-dom
```

## 複習

#🧠 瀏覽器對於URL變動時的預設處理會是什麼？ ->->-> `向對應端點發送新的請求來索求新網頁`
<!--SR:!2022-11-12,10,250-->

#🧠 Single-Page Application 若要實現Client-Side Routing 的話，具體概念是什麼？？ ->->-> `SPA + routing 本身來說會監聽URL變動，若變動就從客戶端的JS bundle 和 實體webpage檔案來產生對應的虛擬webpage頁面，並於瀏覽器直接呈現，在這裡，客戶端並不會為了URL而索要對應的實體webpage頁面`
<!--SR:!2022-11-12,10,250-->

#🧠 Single-Page Application 若要實現Client-Side Routing 的話，具體概念是透過JS bundle 和實體webpage檔案來產生對應的虛擬webpage頁面，那麼若要實現的話，得做什麼？講概念就好->->-> `1. 必須關閉瀏覽器對於URL變動的預設處理 2. 要有程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage。`
<!--SR:!2022-11-12,10,250-->

#🧠 React 上的SPA通常會使用什麼來實現Client-Side Routing ？ ->->-> `react-router`
<!--SR:!2022-11-12,10,250-->

#🧠 React的react-router 是什麼？ ->->-> `實現client-side routing 的第三方套件`
<!--SR:!2022-12-09,28,250-->

#🧠 React的react-router 是官方套件嗎？ ->->-> `不是，第三方套件`
<!--SR:!2022-12-05,25,250-->


#🧠 react-router 和 react-router-dom 之間關係是什麼？ ->->-> `前者是原包含react-router-dom的程式模組，專注提供router功能給調用者，而react-router-dom是從前者抽離出來的dom版本實現代碼，專門呼叫前者來獲取對應功能給DOM介面。`
<!--SR:!2022-11-11,10,250-->


#🧠  react-router 和react-router-dom 提供的功能是什麼？  ->->-> ` 其中react-router本身分為react-router和react-router-dom，前者是負責提供router的核心功能，後者是基於前者的基礎來向DOM渲染介面提供對應router的功能`
<!--SR:!2022-12-06,26,250-->





---
Status: #🌱 
Tags:
[[React]]
Links:
[[client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務；server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務]]
[[SPA 未使用Routing 技術會有的現象：不管我們使用哪些服務或者瀏覽哪些頁面，URL都不會改變，這些服務和頁面都共享著同一個URL。]]
References:
[[@reactrouterFeatureOverviewV6]]