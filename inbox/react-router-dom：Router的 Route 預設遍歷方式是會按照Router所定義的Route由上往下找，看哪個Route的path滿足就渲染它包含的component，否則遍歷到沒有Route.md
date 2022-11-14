## 描述

### Router 的 Route 預設遍歷方式

假若沒使用switch 元件的話，而採取預設遍歷方式：
- 其遍歷的觸發時間是：當目前綁定Router的實體webpage發生URL變動時
- 遍歷：
	- 會按照Router所定義的Route由上往下找，其path matching的實現會是由Route元件來決定，可以是fuzzy matching 或者 exact matching 來比對變動後的URL和path是否一樣。
	- 當變動後的URL滿足當前Route所指定的path，就以Route包含的後裔節點來渲染，接著再往下找下一個Route來比對，直到沒Route可遍歷
	- 當變動後的URL不滿足當前Route所指定的path，就再往下找下一個Route來比對，直到沒Route可遍歷

### Route 的 path matching


> exact: bool
> When true, will only match if the path matches the location.pathname exactly.


重點：
- 若在Route元件添加exact，當被Router挑選到Route時，會以exact matching來比對目前URL和path所指定的路徑是否完全一致
```
<Route path="..." exact />
```
- 若沒在Route元件上添加exact，當被Router挑選到Route時，會以path版本的正規表達式來比對目前URL和path所指定的路徑是否在表達式上達成一致
```
<Route path="..." />
```
#### 在同一個虛擬webpage上，若多個Route的path被滿足的話

在同一個虛擬webpage上，若多個Route的path被滿足的話，就會共同在同一個虛擬webpage上按照滿足的Route所包含的Component來渲染，比如說以下兩個被滿足的Route
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
<!--SR:!2022-11-15,10,250-->

#🧠 react-router：Router 的 Route預設遍歷方式是何時被觸發？->->-> `當目前綁定Router的實體webpage發生URL變動時`
<!--SR:!2022-11-16,10,250-->

#🧠 react-router：Router 的 Route預設遍歷方式是當目前綁定Router的虛擬webpage發生URL變動時嗎？這是正確的嗎->->-> `不正確，實際上是當目前綁定Router的實體webpage發生URL變動時`
<!--SR:!2022-11-16,10,250-->


#🧠 react-router：當變動後的URL滿足當前Route所指定的path，就以Route包含的後裔節點來渲染，那麼就停止遍歷了嗎？為什麼？ ->->-> `並不會停止遍歷，只會繼續往下找Route來比對，直到沒Route可遍歷`
<!--SR:!2022-11-14,9,250-->


#🧠 eact-router：當變動後的URL不滿足當前Route所指定的path，那麼就停止遍歷了嗎？為什麼？ ->->-> `並不會停止遍歷，只會繼續往下找Route來比對，直到沒Route可遍歷`
<!--SR:!2022-11-14,9,250-->

#🧠 react-router：若Route 元件添加exact，那麼會有什麼樣效果？ ->->-> `當被Router挑選到Route時，會以exact matching來比對目前URL和path所指定的路徑是否完全一致`
<!--SR:!2022-12-07,23,250-->

#🧠 react-router：若要讓Route 元件比對path是以exact matching來進行，請問語法會是什麼？->->-> `<Route path="..." exact />`
<!--SR:!2022-12-08,24,250-->


#🧠 react-router：若Route 元件沒添加exact，那麼會有什麼樣效果？ ->->-> `當被Router挑選到Route時，會以path版本的正規表達式來比對目前URL和path所指定的路徑是否在表達式上達成一致`
<!--SR:!2022-11-14,9,250-->


#🧠 react-router：若要讓Route 元件比對path是以path版本的正規表達式來進行，請問語法會是什麼？->->-> `<Route path="..." />`
<!--SR:!2022-11-14,9,250-->


#🧠 react-router：在同一個虛擬webpage上，若多個Route的path被滿足的話，那麼會有什麼樣的效果 ->->-> `就會共同在同一個虛擬webpage上按照滿足的Route所包含的Component來渲染`
<!--SR:!2022-12-01,19,250-->


#🧠 react-router：在同一個虛擬webpage上，若以下2個Route的path被滿足的話，那麼會有什麼樣的效果![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667308798/blog/react/react-router/Route-component/two-paths-react-router-route_dxxb2b.png)->->-> `<Component1 /><Component2 />`
<!--SR:!2022-11-15,10,250-->

#🧠 假如path2、path3是滿足現在切換後的URL1，那麼當URL切換成URL1時的情況會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667308798/blog/react/react-router/Route-component/four-paths-react-router-route_enznvc.png)->->-> `那麼當URL切換成URL1時，就會往目前頁面對應綁定的Router Route定義來往下遍歷：首先是綁定path1的Route進行path比對，結果是不滿足，接著往綁定path2的Route進行path比對，結果是滿足的，並且以Component2 來渲染。接著滿足後就往下找綁定path3的Route來比對path，結果是滿足的，並且以Component3 來渲染，最後再遍歷綁定path4的Route來比對path，結果是不滿足的。`
<!--SR:!2022-11-15,10,250-->


#🧠 假如path2、path3是滿足現在切換後的URL1，那麼當URL切換成URL1時的渲染畫面會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667308798/blog/react/react-router/Route-component/four-paths-react-router-route_enznvc.png)->->->  `<Component2 /><Component3 />`
<!--SR:!2022-12-09,25,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
[[React若在自製Component標籤上添加無屬性(attribute value)值的屬性名稱(attribute)的話，其標籤上的屬性名稱會被賦予true值]]
References: