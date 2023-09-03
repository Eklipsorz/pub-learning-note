## 描述

Server-Side Rendering 指的是 在Client-Server情景下，由伺服器主要負責建立可於瀏覽器視覺呈現的事物，事物會是指代表畫面的實體webpage文件

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

當Client 從伺服器獲得初始網頁後，便會從該網頁發送其他種類的請求，而伺服器接收到請求就會按照上述流程來產生對應的網頁給客戶端

![](https://s3.ap-south-1.amazonaws.com/storage.alfabolt.com/b1e61443-a5b0-4e35-86e2-4f1ad13f657d-min.png)

### Page 組成：
全部皆由實體Webpage檔案實現

### 所能實現的網頁應用程式會是

由於每個URL都對應著實體Hypertext 文件，所以具體會是MPA


#### 優點

[[@alifarooqServerSideRendering]]
> ## Performance

> Server side rendering generally outperforms client side rendering in initial load times. There are still countless cases where CSR is necessary e.g. facebook wouldn’t want to server their entire feed with SSR. The initial load would probably be with server side rendering and additional content can be populate with CSR. So in most real world scenarios, you would be using a combination of SSR and CSR.

> ## SEO

> While Google, Bing and most other search engines have started crawling async javascript applications, your content is still not as likely to be crawled when compared to a page that has its HTML already generated. Server side rendering will always be more reliable and since search engines only allocate a limited time slice to each site to crawl content, your content is more likely to be crawled if search engine does not have to run additional javascript to get to your content.

> ## Social sharing

> Facebook, twitter etc. allow web pages to set snippets of what your site would look like when shared on these platforms. Other applications such as Slack, Linkedin etc. also make use of these tags to show snippets. Social platforms will not run your javascript to generate these snippers so SSR plays an important role here.


這技術的優點：
- 與Client-Side Rendering 相比，webpage所需要載入的JS、CSS、圖片(等另外發送請求載入的資源)的成本會比較少：SSR的每個頁面畫面都對應著實體Hypertext 文件，只需要按照該文件的指示來索要資源，由於CSR本質上會以少量的實體webpage文件為主，並且為了從這些這文件更快地延伸額外內容而預先加載網頁大部分所需要的資源
- SEO 會比Client-Side Rendering 來得好：由於搜尋引擎會利用爬蟲程式來對網頁內容來決定與哪些關鍵字有關聯，通常會比對網頁的靜態內容：不需要執行JS來獲取主要渲染內容，而SSR憑藉以現成的靜態內容而比CSR擁有更好的SEO
- 對應URL都會對應著實體hypertext文件，不需要透過客戶端執行JS來產生對應的虛擬hypertext。


##### SEO 會比Client-Side Rendering 來得好 這句話恐怕未來不為真

部分搜尋引擎的爬蟲有開始針對CSR而採取額外的措施來獲取內容：
	- 爬蟲執行JS來獲取主要內容，並針對內容進行分析

#### 缺點


這技術的缺點：
- Server-side rendering 切換網頁成本比較慢以及比較耗成本：由於只要客戶端一發送請求，無論請求內容大小以要啥，伺服器都直接拿完整網頁傳遞至客戶端，而不是只拿到請求的變更內容。
- 伺服器的效能消耗較大：由於網頁的大部分所需要的計算都會在伺服器上
- 前後端程式碼較難維護：由於程式碼會由於前後端皆於後端實現，所以容易混雜在一起而導致難以維護

#### 適用場景：

[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]
> -   **低頻操作但需要 SEO 優化的網站**：像是媒體類型的網站，因為文章需要被搜尋到，我們看一篇文章也需要一點時間很少高頻的操作這個網站

重點：
- 適用場景為：低頻率切換不同頁面且需要SEO 優化的網站，低頻率意味著需要伺服器做渲染的成本就跟著變低

## 複習

#🧠 Server-Side Rendering 是什麼？(務必講到事物)->->-> `指的是 在Client-Server情景下，由伺服器主要負責建立可於瀏覽器視覺呈現的事物，事物會是指代表畫面的實體webpage文件`
<!--SR:!2023-12-17,252,250-->

#🧠 Server-Side Rendering 是什麼？->->-> `指的是 在Client-Server情景下，由伺服器主要負責建立可於瀏覽器視覺呈現的事物，事物會是指代表畫面的實體webpage文件`
<!--SR:!2024-11-22,461,250-->

#🧠 Server-Side Rendering ：瀏覽器獲取到由伺服器製作的初始網頁之後會做些什麼？ ->->-> `便會從該網頁發送其他種類的請求，而伺服器接收到請求就會按照上述流程來產生對應的網頁給客戶端`
<!--SR:!2023-12-13,101,230-->

#🧠 Server Side Rendering 在client-server情景下是什麼流程？ ->->-> `1. 瀏覽器針對特定網址送出請求 2. 路由器解析請求後，轉接給對應的 controller 3. controller 按照要求，透過 model 拿資料 4. controller 拿到資料後，呼叫 view template，並嵌入資料 5. 把「有資料的 template」轉換成瀏覽器可直接呈現的形式並回傳給瀏覽器 6. 瀏覽器接收檔案並以視覺形式來呈現其畫面。`
<!--SR:!2023-12-14,155,230-->

#🧠 Server Side Rendering 在client-server情景下是什麼流程？請用畫面來表示->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1633596645/blog/network/ClientAndServer/MVCModel_dgvnhm.png)`
<!--SR:!2024-08-20,399,250-->

#🧠 Server Side Rendering 在client-server情景下所擁有的優點是什麼？(共三個)->->-> `SEO 會比Client-Side Rendering 來得好、對應URL都會對應著實體hypertext文件，不需要透過客戶端執行JS來產生對應的虛擬hypertext、 與Client-Side Rendering 相比，webpage所需要載入的JS、CSS、圖片(等另外發送請求載入的資源)的成本會比較少`
<!--SR:!2024-09-01,376,230-->





#🧠  Server Side Rendering 在client-server情景下為何會比Client Side Rendering 擁有較好的SEO???? ->->-> `SEO 會比Client-Side Rendering 來得好：由於搜尋引擎會利用爬蟲程式來對網頁內容來決定與哪些關鍵字有關聯，通常會比對網頁的靜態內容：不需要執行JS來獲取主要渲染內容，而SSR憑藉以現成的靜態內容而比CSR擁有更好的SEO`
<!--SR:!2024-11-20,456,250-->

#🧠 Server-Side Rendering 在每個URL下都對應著什麼？需不需要由客戶端負責什麼？ ->->-> `對應URL都會對應著實體hypertext文件，不需要透過客戶端執行JS來產生對應的虛擬hypertext。`
<!--SR:!2024-11-29,462,250-->


#🧠 Server-Side Rendering 的SEO 會一直比Client-Side Rendering 來得好嗎？為什麼 ->->-> `不一定，由於部分搜尋引擎的爬蟲有開始針對CSR而採取額外的措施來獲取內容，爬蟲執行JS來獲取主要內容，並針對內容進行分析`
<!--SR:!2024-03-13,303,250-->

#🧠 Server-Side Rendering的缺點是什麼？(共三個) ->->-> `切換網頁成本比較慢以及比較耗成本、伺服器的效能消耗較大、前後端程式碼較難維護`
<!--SR:!2023-10-03,29,190-->

#🧠 Server Side Rendering 在client-server情景下為何與Client-Side Rendering 相比，webpage所需要載入的額外資料會比較少？？ ->->-> `SSR的每個頁面畫面都對應著實體Hypertext 文件，只需要按照該文件的指示來索要資料，由於CSR本質上會以少量的實體webpage文件為主，並且為了從這些文件更快地延伸額外內容而預先加載網頁大部分所需要的資源`
<!--SR:!2024-11-27,464,250-->


#🧠 Server-Side Rendering的缺點是切換網頁成本比較慢和比較耗成本，具體說明 ->->-> `由於只要客戶端一發送請求，無論請求內容大小以要啥，伺服器都直接拿完整網頁傳遞至客戶端，而不是只拿到請求的變更內容。`
<!--SR:!2023-11-26,92,230-->

#🧠 Server-Side Rendering的缺點是伺服器的效能消耗較大，具體說明 ->->-> `由於網頁的大部分所需要的計算都會在伺服器上`
<!--SR:!2024-08-17,399,250-->


#🧠 Server-Side Rendering的缺點是前後端程式碼較難維護，具體說明 ->->-> `由於程式碼會由於前後端皆於後端實現，所以容易混雜在一起而導致難以維護`
<!--SR:!2024-08-19,398,250-->

#🧠  Server-Side Rendering 所能實現的網頁應用程式會是？為什麼？ ->->-> `MPA，由於每個URL都對應著實體Hypertext 文件`
<!--SR:!2024-04-09,319,250-->

#🧠 Server-Side Rendering 適用場景為何 ->->-> `低頻率使用且需要SEO 優化的網站`
<!--SR:!2024-03-10,236,230-->

#🧠 Server-Side Rendering 的page 組成是什麼？ ->->-> `全由實體webpage檔案組成`
<!--SR:!2024-08-07,391,250-->


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
[[Server Side Rendering 會是指每一次客戶端向伺服器發送請求時，伺服器都會根據請求內容來將資料與模板網頁檔案做結合網頁，最後由伺服器將結果檔案回傳給客戶端]]
[[Single Page Application 概念上是以一個 實體 webpage 檔案為主體而構成的應用程式；Multiple-Page Application 概念上是以多個 實體webpage 檔案為主體而構成的應用程式]]
[[webpage本身的確能包含JS、圖片、CSS並一同在同一個伺服器回傳，但會使載入資源的壓力容易集中在同一個伺服器上，所以為此會將JS、圖片、CSS存放在其他伺服器來分攤壓力]]
References:
[[@alifarooqServerSideRendering]]
[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]