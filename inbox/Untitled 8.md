## 描述

### Router 的 Route 預設遍歷方式

假若沒使用switch 元件的話，而採取預設遍歷方式：
- 其遍歷的觸發時間是：當目前綁定Router的webpage發生URL變動時
- 遍歷：
	- 會按照Router所定義的Route由上往下找，其path matching的實現會是由Route元件來決定，可以是fuzzy matching 或者 exact matching 來比對變動後的URL和path是否一樣。
	- 當變動後的URL滿足當前Route所指定的path，就以Route包含的後裔節點來渲染，接著再往下找下一個Route來比對，直到沒Route可遍歷
	- 當變動後的URL不滿足當前Route所指定的path，就再往下找下一個Route來比對，直到沒Route可遍歷

### Route 的 path matching


> exact: bool
> When true, will only match if the path matches the location.pathname exactly.


重點：
- 若在Route元件添加exact
```
<Route path="..." exact />
```

#### 若多個Route被滿足的話

若多個Route被滿足的話，就會共同在同一個虛擬webpage上渲染多個Component1，比如說以下兩個被滿足的Route
```
<Route path="path1">
	<Component1 />
</Route>

<Route path="path2">
	<Component2 />
</Route>
```

渲染後的結果會等同於
```
<Component1 />
<Component2 />
```

#### 案例

假如path2、path3是滿足現在切換後的URL1，那麼當URL切換成URL1時，就會往目前頁面對應綁定的Router Route定義來往下遍歷：首先是綁定path1的Route進行path比對，結果是不滿足，接著往綁定path2的Route進行path比對，結果是滿足的，並且以Component2 來渲染

接著滿足後就往下找綁定path3的Route來比對path，結果是滿足的，並且以Component3 來渲染，最後再遍歷綁定path4的Route來比對path，結果是不滿足的。

```
<Route path="path1">
	<Component1 />
</Route>

<Route path="path2">
	<Component2 />
</Route>

<Route path="path3">
	<Component3 />
</Route>

<Route path="path4">
	<Component4 />
</Route>
```

## 複習


#🧠 react-router ：當目前綁定Router的webpage發生URL變動時，Router會做什麼？ ->->-> `會按照Router所定義的Route由上往下找、當變動後的URL滿足當前Route所指定的path，就以Route包含的後裔節點來渲染，接著再往下找下一個Route來比對，直到沒Route可遍歷、當變動後的URL不滿足當前Route所指定的path，就再往下找下一個Route來比對，直到沒Route可遍歷`

#🧠 react-router：Router 的 Route預設遍歷方式是何時被觸發？->->-> `當目前綁定Router的webpage發生URL變動時`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``



#🧠 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667308798/blog/react/react-router/Route-component/two-paths-react-router-route_dxxb2b.png)->->-> ``

#🧠 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667308798/blog/react/react-router/Route-component/four-paths-react-router-route_enznvc.png)->->-> ``



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References: