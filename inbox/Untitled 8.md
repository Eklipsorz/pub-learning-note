## 描述

Client-Side Rendering 是指在Client-Server 場景下，由client端主要負責建立能在自身平台以視覺呈現的事物，該事物會以代表畫面的virtual DOM 或者 DOM來表示。



### 具體實現概念

為了讓client端能夠靠自身建立視覺呈現的事物

具體流程會是：
- client 端先向伺服器1索要特定網頁A
- client一接收到特定網頁A，就要求伺服器2獲取對應JS bundle
- client一接收到JS bundle 就依照目前的互動種類向伺服器3索要資料並渲染初始畫面

隨後client就憑藉JS bundle和網頁A來向指定伺服器索要資料來在客戶端渲染出不同URL所對應的page畫面

![](https://s3.ap-south-1.amazonaws.com/storage.alfabolt.com/b1e61443-a5b0-4e35-86e2-4f1ad13f657d-min.png)


#### 伺服器1 vs. 伺服器2 vs 伺服器3

#####  職責
- 伺服器1是主要提供特定網頁A給客戶端的伺服器
- 伺服器2是主要提供特定網頁A所需要的JS bundle的伺服器
- 伺服器3是主要提供資料來方便讓client憑藉著特定網頁A和JS bundle 來渲染出不同URL所應該要有的page畫面，page會是虛擬的

##### 會是一樣嗎？

伺服器1、伺服器2、伺服器3可以是不一樣的主機或者是全由同一台主機負責。



### 優點

> ## ➤ 優點：

> -   **減少 server 端的壓力**：因為 JS 及 CSS 在第一次都已經發送到 client 端，之後只需要向 server 端取得相關頁面的 data 即可
> -   **頁面切換速度快**：因為 HTML 頁面都是 client 端自己編譯的，所以頁面切換時不需要像 SSR 等待 server 回傳 HTML；而且網頁內容的改變通常都是局部的，這樣就避免了不必要的跳轉及重複渲染。


### 缺點

> ## ➤ 缺點：

> -   **首屏顯示慢**：明明首頁只有一點內容卻把下載了所有頁面的資源
> -   _SEO 較差_：因一開始的 HTML 是空白的，雖然現在 Google 的爬蟲也會等 javascript 編譯好再爬，但這塊對 SEO 的實際幫助還需要時間驗證

- 前端開發成本變高：由於該架構本身Client Side Rendering，所以會根據使用者行為來向後端要資料並處理相關渲染所需的邏輯計算和控制流程來產生對應的畫面至瀏覽器呈現

- 責任分明，容易有推卸的責任

- SEO 會較為糟糕：因為該架構的內容主要會是依據使用者動態調整，而SEO的爬蟲主要是擷取網站的靜態內容來計算和排序，這導致爬蟲能抓的內容是有限的，分數會較低以及排序排得較後面




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@lindingyuanSSRCSRMingCiLiJieYingYongChangJing]]