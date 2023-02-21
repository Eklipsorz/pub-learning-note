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


#### Route 
1. Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component
2. 以wrapper component形式來註冊對應path和對應path所能渲染的元件
	
3. 使用方式為
	- path 要註冊的path 端點，格式會是absolute url 或者 relative url，詳細位置會是以瀏覽器的規則來解析決定
	- Component1： 指定當客戶端的URL端點為path 時，要渲染的Component是什麼
```
import { Route } from 'react-router-dom'; 

return (
	<Route path="/xxx1">
		<Component1 />
	</Route>
)
```

##### 案例
```
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
);
```

```
function App() {
  return (
    <div>
      <MainHeader />
      <Route path='/welcome'>
        <Welcome />
      </Route>
      <Route path='/products'>
        <Products />
      </Route>
    </div>
  );
}
```

### component 若要以虛擬webpage來呈現的話

若component是以虛擬webpage來呈現的話
- 可以存放在/src/pages 或者 /src/screens
以此來讓開發者區分出哪些元件作為一般component來使用？哪些元件是作為虛擬webpage來使用並呈現

## 複習

#🧠 react-router-dom v5中：BrowserRouter 是什麼？功能是什麼 ->->-> `BrowserRouter 是一個component，主要提供client-side routing服務的component`
<!--SR:!2023-08-06,176,250-->

#🧠 react-router-dom v5中：BrowserRouter 是一個component，主要提供client-side routing服務的component，那麼如何使元件們能享用這項服務 ->->-> `以wrapper component形式來包含後裔元件或者子元件，使他們都能使用client-side routing服務`
<!--SR:!2023-02-22,74,250-->

#🧠 react-router-dom v5中：BrowserRouter 是一個component，主要提供client-side routing服務的component，那麼如何使元件們能享用這項服務，使用方式是？(包含載入)->->-> `import { BrowserRouter } from 'react-router-dom';  <BrowserRouter> <Component /> <BrowserRouter />`
<!--SR:!2023-08-24,186,250-->


#🧠 react-router-dom v5中：BrowserRouter 要如何載入？ ->->-> `import { BrowserRouter } from 'react-router-dom'; `
<!--SR:!2023-02-22,74,250-->

#🧠 react-router-dom v5中：如何定義router 的 route?  ->->-> `使用Route component 來定義哪個path所對應的component是什麼？`
<!--SR:!2023-08-05,176,250-->

#🧠 react-router-dom v5中：Route 是什麼？功能是？->->-> `Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component`
<!--SR:!2023-08-27,188,250-->

#🧠 react-router-dom v5中：Route 元件如何定義path和對應的component？(包含載入) ->->-> `import { Route } from 'react-router-dom'; return ( <Route path="/xxx1"> <Component1 /> </Route>）`
<!--SR:!2023-02-23,75,250-->

#🧠 react-router-dom v5中：Route 元件的path 和 Component1是什麼？ ->->-> ` path 要註冊的path 端點和Component1： 指定當客戶端的URL端點為path 時，要渲染的Component是什麼`
<!--SR:!2023-08-25,186,250-->


#🧠  react-router-dom v5中：Route 元件的 path 格式是什麼？ ->->-> `path 要註冊的path 端點，格式會是absolute url 或者 relative url，詳細位置會是以瀏覽器的規則來解析決定`
<!--SR:!2023-02-22,74,250-->

#🧠 react-router-dom v5中：Route 元件的 path 通常是以哪個實際path為主？ ->->-> `其端點以react app所在的實際URL位置為主`
<!--SR:!2023-02-21,73,250-->

#🧠 react-router-dom v5中：Route 元件的 path設定為/apple，那react app URL位置為xxxx1.com，那麼URL是什麼才能到/apple所設定的路徑->->-> `xxxx1.com/apple 來看待。`
<!--SR:!2023-02-21,73,250-->



#🧠 react-router-dom v5中：Route 元件要如何被載入？ ->->-> `import { Route } from 'react-router-dom'; `
<!--SR:!2023-09-01,192,250-->


#🧠 下面案例為已經使用BrowserRouter來建立的路徑，請說明該路由系統的那兩個路徑會是什麼意思？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667045564/blog/react/react-router/react-router-example_qbq28a.png): ->->-> ``
<!--SR:!2023-02-22,74,250-->


#🧠 React：component 若要以虛擬webpage來呈現的話，開發者要如何區分？->->-> `將該component放置在/src/pages 或者 /src/screens`
<!--SR:!2023-02-23,75,250-->

#🧠 React：\/src\/pages 存放什麼？  ->->-> `存放專門擔任對應頁面所對應的虛擬webpage之component`
<!--SR:!2023-08-14,180,250-->

---
Status: #🌱
Tags:
[[React]]
Links:
[[SPA 實現client-side routing的概念，具體是要必須關閉瀏覽器對於URL變動的預設處理和程式模組負責監聽URL變動以及按變動後的URL來產生對應的虛擬webpage]]
[[client-side routing 主要是由客戶端自己根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務；server-side routing 主要由伺服器根據瀏覽器的URL變動來產生對應的webpage提供畫面和服務]]
[[SPA 未使用Routing 技術會有的現象：不管我們使用哪些服務或者瀏覽哪些頁面，URL都不會改變，這些服務和頁面都共享著同一個URL。]]
[[relative URL 會是以特定資源A的所在目錄位置為參考點來找到特定資源B的路徑，特定路徑A通常會是以特定資源A的所在目錄位置為參考點來指定]]
[[absolute URL：意指為特定資源在網路上的完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置]]
References:
[[@react-routerReactRouterDeclarativea]]