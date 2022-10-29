## 描述

### react-router-dom v5


#### BrowserRouter 
1. BrowserRouter 是一個component，主要提供client-side routing服務的component
2. 以wrapper component形式來包含後裔元件或者子元件，使他們都能使用client-side routing服務
3. 使用方式會是：
```
import { BrowserRouter } from 'react-router-dom'; 

return (
	<BrowserRouter> 
		<Component />
	<BrowserRouter />
)
```

### 由Router 元件負責定義basepath
主要有兩種Router：
- BrowserRouter
- HashRouter
##### 由BrowserRouter 負責定義basepath

[[@react-routerReactRouterDeclarative]]
> A \<Router\> that uses the HTML5 history API (pushState, replaceState and the popstate event) to keep your UI in sync with the URL.


> basename: string
> The base URL for all locations. If your app is served from a sub-directory on your server, you’ll want to set this to the sub-directory. A properly formatted basename should have a leading slash, but no trailing slash.

example
```jsx
<BrowserRouter basename="/calendar">
    <Link to="/today"/> // renders <a href="/calendar/today">
    <Link to="/tomorrow"/> // renders <a href="/calendar/tomorrow">
    ...
</BrowserRouter>
```

重點：
- 若採用BrowserRouter 架構的路由結構，會由BrowserRouter來定義basepath
- basepath主要是設定
	- 其架構的路由結構會以什麼實際路徑作為base path或root 

#### Route 
1. Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component
2. 以wrapper component形式來註冊對應path和對應path所能渲染的元件，具體會是當URL 變動時：
		- router 會掃描每個Route 所定義的path是否滿足，若滿足的話，就以對應的元件來渲染，並停止掃描；
		- 若不滿足的話，就會查找下一個Route，一直到找到或者找不到而顯示空白
	
3. 使用方式為
	- path 要註冊的path 端點，格式會是/xxxx，其中xxxx為端點，其端點以react app所在的實際URL位置為主，比如說react app URL位置為xxxx1.com，那麼端點會以xxxx1.com/xxxx 來看待。
	- Component1： 指定當客戶端的URL端點為path 時，要渲染的Component是什麼
```
import { Route } from 'react-router-dom'; 

return (
	<Route path="/xxx1">
		<Component1 />
	</Route>
)
```

### component 若要以虛擬webpage來呈現的話

若component是以虛擬webpage來呈現的話
- 可以存放在/src/pages 或者 /src/screens
以此來讓開發者區分出哪些元件作為一般component來使用？哪些元件是作為虛擬webpage來使用並呈現

## 複習

#🧠 react-router-dom v5中：BrowserRouter 是什麼？功能是什麼 ->->-> `BrowserRouter 是一個component，主要提供client-side routing服務的component`

#🧠 react-router-dom v5中：BrowserRouter 是一個component，主要提供client-side routing服務的component，那麼如何使元件們能享用這項服務 ->->-> `以wrapper component形式來包含後裔元件或者子元件，使他們都能使用client-side routing服務`

#🧠 react-router-dom v5中：BrowserRouter 是一個component，主要提供client-side routing服務的component，那麼如何使元件們能享用這項服務，使用方式是？(包含載入)->->-> `import { BrowserRouter } from 'react-router-dom';  <BrowserRouter> <Component /> <BrowserRouter />`


#🧠 react-router-dom v5中：BrowserRouter 要如何載入？ ->->-> `import { BrowserRouter } from 'react-router-dom'; `

#🧠 react-router-dom v5中：如何定義router 的 route?  ->->-> `使用Route component 來定義哪個path所對應的component是什麼？`

#🧠 react-router-dom v5中：Route 是什麼？功能是？->->-> `Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component`

#🧠 react-router-dom v5中：Route 元件如何定義path和對應的component？(包含載入) ->->-> `import { Route } from 'react-router-dom'; return ( <Route path="/xxx1"> <Component1 /> </Route>）`

#🧠 react-router-dom v5中：path 和 Component1是什麼？ ->->-> ` path 要註冊的path 端點和Component1： 指定當客戶端的URL端點為path 時，要渲染的Component是什麼`


#🧠  react-router-dom v5中：Route 元件的 path 格式是什麼？ ->->-> `格式為/xxxx，xxxx為端點`

---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
[[SPA 實現client-side routing的概念，具體是要必須關閉瀏覽器對於URL變動的預設處理和程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage]]
[[client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務；server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務]]
[[SPA 未使用Routing 技術會有的現象：不管我們使用哪些服務或者瀏覽哪些頁面，URL都不會改變，這些服務和頁面都共享著同一個URL。]]
References:
[[@react-routerReactRouterDeclarativea]]