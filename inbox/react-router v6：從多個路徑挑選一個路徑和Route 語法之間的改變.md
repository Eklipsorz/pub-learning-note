


## 描述

> A \<Route\> is only ever to be used as the child of \<Routes\> element, never rendered directly. Please wrap your \<Route\> in a \<Routes\>.

[[@react-routerReactRouterDeclarativea]]
> Upgrade all \<Switch\> elements to \<Routes\>
> React Router v6 introduces a Routes component that is kind of like Switch, but a lot more powerful.


### v5 vs. v6 ：從多個路徑挑選一個路徑

v5 ：
- 是使用Switch元件＋多個Route元件來實現
v6 ：
- 丟棄Switch元件
- 是使用Routes元件＋多個Route元件來實現


#### v5：Switch 挑選路徑方式
Switch 元件 在挑選路徑時會以誰先滿足目前URL來挑選，流程為
- 遍歷每個Route元件並比對目前它的path和URL是否滿足，
	- 若滿足就挑它並停止遍歷
	- 若不滿足就繼續遍歷

#### v6：Routes 挑選路徑方式
Routes 元件 在挑選路徑時會以具體程度為優先來挑選，流程為：
- 遍歷每個Route元件並評估目前Route元件所對應的path 對於目前URL的具體程度為何
- 遍歷完就以具體程度最高的Route元件為主


### Routes 簡介
[[@react-routerReactRouterDeclarativea]]
> Whenever the location changes, `<Routes>` looks through all its child routes to find the best match and renders that branch of the UI

重點：
- Routes 是個react-router-dom的元件
- 主要用途為管理多個Route元件並為目前URL從管理下的Route元件中挑選出最合適的Route元件來渲染

##### 案例：Routes 挑選路徑方式

若URL切換至/products/edit的話，預期會有兩個路徑會成立並且渲染，但由於會比較具體程度，而最後一個Route設定的路徑是設定明確的路徑，所以會選擇它作為渲染元件。

```
function App() {
  return (
    <div>
      <MainHeader />
      <main>
        <Routes>
          <Route path='/welcome' element={<Welcome />} />
          <Route path='/products' element={<Products />} />
          <Route path='/products/:productId' element={<ProductDetail />} />
          <Route path='/products/edit' element={xxxxx} />
        </Routes>
      </main>
    </div>
  );
}
```


### v5 vs. v6： Route 語法的改變


v6：
1. 每個Route元件都要用Routes元件來包裹
2. 每個Route元件都會是以exact matching來比對path
3. 若要使用fuzzy matching，可以使用\*這字元來表示，比如若要表示welcome開頭的頁面都是渲染element1元件，就設定如下
```
<Route path='/welcome/* element={element1} />
```
4. 語法：
	 - path 屬性是填入要比對的路徑
	 - element 屬性是填入要比對滿足後要渲染的元件
```
<Route path=path1 element={element1} />
```


## 複習


#🧠 react-router v5 vs. v6 ：從多個路徑挑選一個路徑實現概念為何？ ->->-> `v5 ： - 是使用Switch元件＋多個Route元件來實現 v6 ：- 是使用Routes元件＋多個Route元件來實現`

#🧠 react-router v6 : Routes 是具有什麼用途的元件？ ->->-> `管理多個Route元件並為目前URL從管理下的Route元件中挑選出最合適的Route元件來渲染`

#🧠 react-router v6 : Routes 出自於哪裡的元件 ->->-> `react-router-dom的元件`

#🧠 react-router v5：Switch 挑選路徑的主旨會是什麼？ ->->-> `Switch 元件 在挑選路徑時會以誰先滿足目前URL來挑選`

#🧠 react-router v5：Switch 挑選路徑方式會是什麼？->->-> `Switch 元件 在挑選路徑時會以誰先滿足目前URL來挑選：- 遍歷每個Route元件並比對目前它的path和URL是否滿足：- 若滿足就挑它並停止遍歷 - 若不滿足就繼續遍歷`

#🧠 react-router v5：Switch 挑選路徑方式會是遍歷每個Route元件並比對目前它的path和URL是否滿足，若滿足的話，則？ ->->-> `若滿足就挑它並停止遍歷`


#🧠 react-router v5：Switch 挑選路徑方式會是遍歷每個Route元件並比對目前它的path和URL是否滿足，若不滿足的話，則？ ->->-> ` 若不滿足就繼續遍歷`

#🧠 react-router v6：Routes 挑選路徑的主旨會是什麼？ ->->-> `Routes 元件 在挑選路徑時會以具體程度為優先來挑選`


#🧠 react-router v6：Routes 挑選路徑方式會是什麼？ ->->-> `Routes 元件 在挑選路徑時會以具體程度為優先來挑選，流程為： - 遍歷每個Route元件並評估目前Route元件所對應的path 對於目前URL的具體程度為何 - 遍歷完就以具體程度最高的Route元件為主`

#🧠 Switch 元件在react-router上的版本5和版本6是否存在？ ->->-> `僅存在於版本5`

#🧠 react-router v6：每個Route有什麼樣的不同？ ->->-> `使用時都要用Routes來包裹、每個Route元件都會是以exact matching、語法上的不同`


#🧠 react-router v6：每個Route有什麼樣的不同？其中每個Route元件都會是以exact matching，若要用fuzzy matching，那麼可以怎麼做？->->-> `使用/*來表示`


#🧠 react-router v6：每個Route有什麼樣的不同？語法上的不同是指什麼 ->->-> `要渲染的元件會以Route元件的屬性來表示`

#🧠 react-router v6：Route語法標籤是什麼？ ->->-> `<Route path=path1 element={element1} />`


#🧠 react-router v6：Route語法標籤是`<Route path=path1 element={element1} />`，那麼path和element各為什麼？ ->->-> `	 - path 屬性是填入要比對的路徑  - element 屬性是填入要比對滿足後要渲染的元件`


#🧠 假設目前是react-router v6，若URL切換至/products/edit的話，會呈現什麼畫面？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1669900964/blog/react/react-router/v6/react-router-v6-route-example_fhsfsi.png) ->->-> `但由於會比較具體程度，而最後一個Route設定的路徑是設定明確的路徑，所以會選擇它作為渲染元件。`




---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]