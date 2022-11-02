## 描述
[[@react-routerReactRouterDeclarativea]]
> \<Switch\> is unique in that it renders a route _exclusively_. In contrast, every \<Route\> that matches the location renders _inclusively_. Consider these routes


> Route switch 

> Renders the first child \<Route\> or \<Redirect\> that matches the location.
> How is this different than just using a bunch of \<Route\>s?

重點：
- switch 是一個元件，最主要是根據目前切換後的URL和後裔Route元件所擁有path是否滿足或者一樣來決定其渲染的control flow，具體則是當Switch中的任一Route上的path是否滿足於目前切換的path，滿足的話，就跳出Switch以外來停止後續的Route挑選。
- 載入方式：
```
import { Switch } from 'react-router-dom';
```
- 使用方式：
	- 當Switch中的任一Route上的path滿足於目前切換的path，就跳出Switch以外來停止後續的Route挑選
```
<Switch>
	<Route path=path1 />
	<Route path=path2 />
	.
	.
</Switch>
```

### 在沒採用switch 下的Route 遍歷所造成的問題 

切換端點會滿足多個Route而同時在同一個頁面渲染多個Route所包含的component，若使用者對著以下端點進行切換的話，會因為會同時滿足第二個Route和第三個Route所設定的path而將Products元件和ProductDetails元件同時在目前webpage顯示

```
/products/1
```

```
  return (
    <div>
      <MainHeader />
      <Route path='/welcome'>
        <Welcome />
      </Route>
      <Route path='/products'>
        <Products />
      </Route>
      <Route path='/products/:productId'>
        <ProductDetails />
      </Route>
    </div>
  );
```

#### 解法概念
1. 使用Switch 元件 + 改變Route順序：改變的順序是\/products\/\:productId 和 \.products
```
  return (
    <Switch>
      <MainHeader />
      <Route path='/welcome'>
        <Welcome />
      </Route>
      <Route path='/products/:productId'>
        <ProductDetails />
      </Route>
      <Route path='/products'>
        <Products />
      </Route>
    </Switch>
  );
```


2. 使用Switch 元件 ＋ 添加exact matching：添加exact至\/products的Route上，當挑選到它時，就以exact matching來比對目前URL和path是否完全一致，只要有點不一樣，都會被認為不一樣
```
  return (
    <Switch>
      <MainHeader />
      <Route path='/welcome'>
        <Welcome />
      </Route>
      <Route path='/products' exact>
        <Products />
      </Route>
      <Route path='/products/:productId'>
        <ProductDetails />
      </Route>
    </Switch>
  );
```
## 複習

#🧠 react-router-dom：switch 是什麼？做什麼？ ->->-> `switch 是一個元件，最主要是根據目前切換後的URL和後裔Route元件所擁有path是否滿足或者一樣來決定其渲染的control flow`

#🧠 react-router-dom：switch 是一個元件，最主要是根據目前切換後的URL和後裔Route元件所擁有path是否滿足或者一樣來決定其渲染的control flow，具體是什麼？ ->->-> `具體則是當Switch中的任一Route上的path是否滿足於目前切換的path，滿足的話，就跳出Switch以外來停止後續的Route挑選`

#🧠 react-router-dom：switch  如何載入？ ->->-> `import { Switch } from 'react-router-dom';`

#🧠 react-router-dom：switch  使用方式如何？ ->->-> `<Switch> <Route path=path1 /> <Route path=path2 /> . . </Switch>`

#🧠 react-router-dom： 在沒採用switch 下的Route 遍歷所造成的問題會是什麼？ 與Route本身只會在遍歷完畢才停止有關->->-> `切換端點會滿足多個Route而致使同時在同一個頁面渲染多個Route所包含的component`


---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router-dom：Router的 Route 預設遍歷方式是會按照Router所定義的Route由上往下找，看哪個Route的path滿足就渲染它包含的component，否則遍歷到沒有Route]]
References:
[[@react-routerReactRouterDeclarativea]] 