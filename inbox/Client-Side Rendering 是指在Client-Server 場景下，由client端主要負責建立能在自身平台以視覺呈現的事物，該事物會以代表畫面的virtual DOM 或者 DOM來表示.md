## 描述

Client-Side Rendering 是指在Client-Server 場景下，由client端主要負責建立能在自身平台以視覺呈現的事物，該事物會以代表畫面的virtual DOM 或者 DOM來表示。



### 具體實現概念

為了讓client端能夠靠自身建立視覺呈現的事物

具體流程會是：
- client 端先向伺服器1索要特定網頁A
- client一接收到特定網頁A，就要求伺服器2獲取對應JS bundle
- client一接收到JS bundle 就依照目前的互動種類向伺服器3索要資料並渲染初始畫面

隨後client就憑藉JS bundle和網頁A來向指定伺服器索要資料來在客戶端渲染出不同URL所對應的page畫面
[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]
![](https://s3.ap-south-1.amazonaws.com/storage.alfabolt.com/b1e61443-a5b0-4e35-86e2-4f1ad13f657d-min.png)


#### 伺服器1 vs. 伺服器2 vs 伺服器3

#####  職責
- 伺服器1是主要提供特定網頁A給客戶端的伺服器
- 伺服器2是主要提供特定網頁A所需要的JS bundle的伺服器
- 伺服器3是主要提供資料來方便讓client憑藉著特定網頁A和JS bundle 來渲染出不同URL所應該要有的page畫面，page會是虛擬的

##### 會是一樣嗎？

伺服器1、伺服器2、伺服器3可以是不一樣的主機或者是全由同一台主機負責。


### Page 組成：
少量的實體Webpage 和 大量建構出來的虛擬Webpage：
- 實體部分會是指一份實體webpage
- 虛擬部分則會是N份虛擬webpage


### 優點

> ## ➤ 優點：

> -   **減少 server 端的壓力**：因為 JS 及 CSS 在第一次都已經發送到 client 端，之後只需要向 server 端取得相關頁面的 data 即可
> -   **頁面切換速度快**：因為 HTML 頁面都是 client 端自己編譯的，所以頁面切換時不需要像 SSR 等待 server 回傳 HTML；而且網頁內容的改變通常都是局部的，這樣就避免了不必要的跳轉及重複渲染。


重點：
- 減少server處理渲染部分的壓力：因為client 憑藉著一開始就已經獲取到包含著JS和CSS的實體webpage文件，所以可由它主要渲染自身的畫面就好
- 頁面切換較快：由於網頁畫面是由client端自行負責，並不需要再次向伺服器索要新的實體webpage，且能根據不同時機點下的dom內容差異來以dom為單位來轉換畫面

### 缺點

> ## ➤ 缺點：

> -   **首屏顯示慢**：明明首頁只有一點內容卻把下載了所有頁面的資源
> -   _SEO 較差_：因一開始的 HTML 是空白的，雖然現在 Google 的爬蟲也會等 javascript 編譯好再爬，但這塊對 SEO 的實際幫助還需要時間驗證

重點：
- 與Server-Side Rendering 相比，webpage所需要載入的額外資料會比較多：SSR的每個頁面畫面都對應著實體Hypertext 文件，只需要按照該文件的指示來索要資料，由於CSR本質上會以少量的實體webpage文件為主，並且為了從這些這文件更快地延伸額外內容而預先加載網頁大部分所需要的資源
- SEO 會比Server-Side Rendering 來得差：由於搜尋引擎會利用爬蟲程式來對網頁內容來決定與哪些關鍵字有關聯，通常會比對網頁的靜態內容：不需要執行JS來獲取主要渲染內容，而SSR憑藉以現成的靜態內容而比CSR擁有更好的SEO


### 所能實現的網頁應用程式會是

由於本質上只需要少量的實體webpage文件來建構出其他虛擬page，通常少量會是指單個實體webpage文件，因此被稱之為Single-Page Application，所能實現的應用程式就是SPA

### 適用場景
[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]
> **會高頻操作且不需 SEO 的網站**：像是內部管理系統，如果這類型的系統採取 SSR 會造成 server 端很大的負荷。

重點：
- 適用於高頻切換不同頁面且不需要SEO的網頁

## 複習

#🧠 Client-Side Rendering  概念是什麼？ ->->-> `Client-Side Rendering 是指在Client-Server 場景下，由client端主要負責建立能在自身平台以視覺呈現的事物，該事物會以代表畫面的virtual DOM 或者 DOM來表示。`
<!--SR:!2022-10-30,3,250-->

#🧠 Client-Side Rendering  具體流程是什麼？->->-> `- client 端先向伺服器1索要特定網頁A - client一接收到特定網頁A，就要求伺服器2獲取對應JS bundle - client一接收到JS bundle 就依照目前的互動種類向伺服器3索要資料並渲染初始畫面。 隨後client就憑藉JS bundle和網頁A來向指定伺服器索要資料來在客戶端渲染出不同URL所對應的page畫面`
<!--SR:!2022-10-30,3,250-->


#🧠 Client-Side Rendering  具體流程是什麼？用畫圖表示 ->->-> `![](https://s3.ap-south-1.amazonaws.com/storage.alfabolt.com/b1e61443-a5b0-4e35-86e2-4f1ad13f657d-min.png)`


#🧠 Client-Side Rendering  具體流程是：-client 端先向伺服器1索要特定網頁A - client一接收到特定網頁A，就要求伺服器2獲取對應JS bundle - client一接收到JS bundle 就依照目前的互動種類向伺服器3索要資料並渲染初始畫面。 其中伺服器1、伺服器2、伺服器3會是什麼？->->-> `- 伺服器1是主要提供特定網頁A給客戶端的伺服器 - 伺服器2是主要提供特定網頁A所需要的JS bundle的伺服器 - 伺服器3是主要提供資料來方便讓client憑藉著特定網頁A和JS bundle 來渲染出不同URL所應該要有的page畫面，page會是虛擬的`

#🧠 Client-Side Rendering  具體流程是：-client 端先向伺服器1索要特定網頁A - client一接收到特定網頁A，就要求伺服器2獲取對應JS bundle - client一接收到JS bundle 就依照目前的互動種類向伺服器3索要資料並渲染初始畫面。 其中伺服器1、伺服器2、伺服器3會是一樣的嗎？->->-> `伺服器1、伺服器2、伺服器3可以是不一樣的主機或者是全由同一台主機負責。
`

#🧠 Client-Side Rendering 的Page組成是什麼？ ->->-> `少量的實體Webpage 和 大量建構出來的虛擬Webpage：  實體部分會是指一份實體webpage - 虛擬部分則會是N份虛擬webpage`
<!--SR:!2022-10-30,3,250-->

#🧠 Client-Side Rendering 的優點是什麼？(共兩個) ->->-> `減少server處理渲染部分的壓力、頁面切換較快`
<!--SR:!2022-10-30,3,250-->

#🧠 Client-Side Rendering 的優點是減少server處理渲染部分的壓力，具體說明 ->->-> `因為client 憑藉著一開始就已經獲取到包含著JS和CSS的實體webpage文件，所以可由它主要渲染自身的畫面就好`

#🧠 Client-Side Rendering 的優點是頁面切換較快，具體說明 ->->-> `由於網頁畫面是由client端自行負責，並不需要再次向伺服器索要新的實體webpage，且能根據不同時機點下的dom內容差異來以dom為單位來轉換畫面`

#🧠 Client-Side Rendering 的缺點是什麼？(共兩個) ->->-> `與Server-Side Rendering 相比，webpage所需要載入的額外資料會比較多、SEO 會比Server-Side Rendering 來得差`

#🧠 Client-Side Rendering 的缺點是與Server-Side Rendering 相比，webpage所需要載入的額外資料會比較多，具體說明 ->->-> `SSR的每個頁面畫面都對應著實體Hypertext 文件，只需要按照該文件的指示來索要資料，由於CSR本質上會以少量的實體webpage文件為主，並且為了從這些這文件更快地延伸額外內容而預先加載網頁大部分所需要的資源`

#🧠 Client-Side Rendering 的缺點是SEO 會比Server-Side Rendering 來得差，具體說明 ->->-> `由於搜尋引擎會利用爬蟲程式來對網頁內容來決定與哪些關鍵字有關聯，通常會比對網頁的靜態內容：不需要執行JS來獲取主要渲染內容，而SSR憑藉以現成的靜態內容而比CSR擁有更好的SEO`


#🧠 Client-Side Rendering所能實現的網頁應用程式會是？為什麼？ ->->-> `由於本質上只需要少量的實體webpage文件來建構出其他虛擬page，通常少量會是指單個實體webpage文件，因此被稱之為Single-Page Application，所能實現的應用程式就是SPA`

#🧠 Client-Side Rendering適用場景為何 ->->-> `適用於高頻切換不同頁面且不需要SEO的網頁`
<!--SR:!2022-10-30,3,250-->


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]