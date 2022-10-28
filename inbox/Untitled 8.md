## 描述

###

至/src/index.js 來載入模組來讓App 元件擁有client-side routing服務

import { BrowserRouter } from 'react-router-dom'; ：

- BrowserRouter 是一個component，主要提供client-side routing服務的component

- 以wrapper component形式來包含後裔元件或者子元件，使他們都會使用client-side routing服務




### 

import { Route } from 'react-router-dom'：

1. Route 是一個component，主要是定義特定path以及對應path會渲染出來的component

2. 使用方式：

- path 要註冊的path 端點，其URL會是以react app所在的實際URL位置

- Component1： 當客戶端的URL端點為path 時，就只渲染Component1對應的DOM

```
<Route path="xxxx" >
    <Component1> 
</Route>
```


3. 若客戶端的PATH端點並沒符合Route所設定的Path，就會顯示空白

  
若component是以虛擬webpage來呈現的話，可以存放在/src/pages 或者 /src/screens，以此來讓開發者區分出哪些元件作為一般component來使用？哪些元件是作為虛擬webpage來使用並呈現
## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[SPA 實現client-side routing的概念，具體是要必須關閉瀏覽器對於URL變動的預設處理和程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage]]
[[client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務；server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務]]
[[SPA 未使用Routing 技術會有的現象：不管我們使用哪些服務或者瀏覽哪些頁面，URL都不會改變，這些服務和頁面都共享著同一個URL。]]
References: