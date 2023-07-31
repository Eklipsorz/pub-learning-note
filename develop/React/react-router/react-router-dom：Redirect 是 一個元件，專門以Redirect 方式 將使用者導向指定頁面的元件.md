## 描述

[[@react-routerReactRouterDeclarativea]]
> Rendering a `<Redirect>` will navigate to a new location. The new location will override the current location in the history stack, like server-side redirects (HTTP 3xx) do.


> to: string

> The URL to redirect to. Any valid URL path that path-to-regexp@^1.7.0 understands. All URL parameters that are used in to must be covered by from.


重點：
- Redirect 是 一個元件，專門以Redirect 方式 將使用者導向指定頁面的元件
- 元件的使用語法
	- to 是指定要導向頁面的所在位置，可填入relative URL 或者 absoute URL
```
import { Redirect } from 'react-router-dom';

return (

	<Router>
		<Route path="/path1">
			<Redirect to="/path2" />
		</Route>
		<Route path="/path2">
			<Component2 />
		</Route>
	</Router> 
)
```
- 載入方式為：
```
import { Redirect } from 'react-router-dom';
```



#### 範例


```
function App() {
  return (
    <div>
      <MainHeader />
      <Switch>
        <Route path='/' exact>
          <Redirect to='/welcome' />
        </Route>
        <Route path='/welcome'>
          <Welcome />
        </Route>
        <Route exact path='/products'>
          <Products />
        </Route>
        <Route path='/products/:productId/'>
          <ProductDetails />
        </Route>
      </Switch>
    </div>
  );
```

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[redirect 是面向於客戶端的請求處理，主要會要求客戶端導向目標URL所指向的頁面，rewrite 是面向於伺服器端的請求處理，主要會在伺服器正式處理前將封包的端點改寫指定端點，處理時以改寫]]
References:
[[@react-routerReactRouterDeclarativea]]