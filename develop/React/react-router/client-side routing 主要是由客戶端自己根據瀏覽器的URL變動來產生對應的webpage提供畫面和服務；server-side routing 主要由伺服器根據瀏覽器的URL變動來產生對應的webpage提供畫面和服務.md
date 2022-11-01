## 描述



### client-side routing 
[[@reactrouterFeatureOverviewV6]]
> Client side routing allows your app to update the URL from a link click without making another request for another document from the server. Instead, your app can immediately render some new UI and make data requests with `fetch` to update the page with new information.

重點：
- client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務，客戶端不向伺服器的對應端點發送請求索要對應端點的畫面和服務



### server-side routing
- server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務，具體是由客戶端向伺服器的端點發送請求，伺服器接收到請求就回傳webpage來提供畫面和服務



## 複習
#🧠 client-side routing 是什麼樣的技術？->->-> `主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務，客戶端不向伺服器的對應端點發送請求索要對應端點的畫面和服務`
<!--SR:!2022-11-11,10,250-->

#🧠 client-side routing 還會不會向伺服器的對應端點發送請求索要對應端點的畫面和服務 ->->-> `除了一開始的實體webpage載入以外，之後都由客戶端自行處理`
<!--SR:!2022-11-10,9,250-->

#🧠 server-side routing 是什麼樣的技術 ->->-> `server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務`
<!--SR:!2022-11-10,9,250-->

#🧠 server-side routing 是主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務，具體是什麼？ ->->-> `客戶端向伺服器的端點發送請求，伺服器接收到請求就回傳webpage來提供畫面和服務`
<!--SR:!2022-11-10,9,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactrouterFeatureOverviewV6]]