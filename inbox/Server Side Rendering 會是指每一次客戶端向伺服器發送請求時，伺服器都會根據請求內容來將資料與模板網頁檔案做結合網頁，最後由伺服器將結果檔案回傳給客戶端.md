## 描述

### Server Side Rendering

由伺服器一端負責將使用者的請求來轉換成對應的View，而View形式會是**HTML、JS、CSS所構成的網頁畫面**，每一次客戶端向伺服器發送請求時，伺服器都會根據請求內容來將資料與模板網頁檔案做結合並轉換成**客戶端可直接以視覺呈現的檔案**，最後由伺服器將結果檔案回傳給客戶端

> rendering a client-side or universal app to HTML on the server.

簡述流程：
1. 瀏覽器針對特定網址送出請求
2. 路由器解析請求後，轉接給對應的 controller
3. controller 按照要求，透過 model 拿資料
4. controller 拿到資料後，呼叫 view template，並嵌入資料
5. 把「有資料的 template」轉換成瀏覽器可直接呈現的形式並回傳給瀏覽器
6. 瀏覽器接收檔案並以視覺形式來呈現其畫面。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1633596645/blog/network/ClientAndServer/MVCModel_dgvnhm.png)

  

這技術的優點：

- 對客戶端(瀏覽器)要求較低：由於客戶端一拿到手就可以直接呈現，不需要花太多效能成本來將檔案轉換成畫面

這技術的缺點：

- 使用者體驗較差：由於只要客戶端一發送請求，無論請求內容大小以要啥，伺服器都直接拿完整網頁傳遞至客戶端，而不是只拿到請求的變更內容。

- 伺服器的效能消耗較大：由於網頁的大部分所需要的計算都會在伺服器上

- 前後端程式碼較難維護：由於程式碼會由於前後端皆於後端實現，所以容易混雜在一起而導致難以維護


## 複習


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
[[Server Side Rendering 會是指每一次客戶端向伺服器發送請求時，伺服器都會根據請求內容來將資料與模板網頁檔案做結合網頁，最後由伺服器將結果檔案回傳給客戶端]]
[[Single Page Application 概念上是以一個 實體 webpage 檔案為主體而構成的應用程式；Multiple-Page Application 概念上是以多個 實體webpage 檔案為主體而構成的應用程式]]
References: