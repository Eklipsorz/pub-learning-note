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
```
<BrowserRouter basename="/calendar">
	// renders <a href="/calendar/today">
    <Link to="/today"/> 
    // renders <a href="/calendar/tomorrow">
    <Link to="/tomorrow"/> 
    ...
</BrowserRouter>
```

重點：
- 若採用BrowserRouter 架構的路由結構，會由BrowserRouter來定義basepath
- basepath主要是設定
	- 其架構的路由結構會以什麼實際路徑作為base path或root path
	- basepath 預設會是 \/
- 案例：假設BrowserRouter 路由架構主要是由兩個Route所構成
	- 
```
<BrowserRouter basename="/calendar">
	// renders <a href="/calendar/today">
    <Link to="/today"/> 
    // renders <a href="/calendar/tomorrow">
    <Link to="/tomorrow"/> 
    ...
</BrowserRouter>
```
