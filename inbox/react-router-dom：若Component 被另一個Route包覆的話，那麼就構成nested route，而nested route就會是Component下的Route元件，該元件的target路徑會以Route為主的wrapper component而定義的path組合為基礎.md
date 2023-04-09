## 描述


### nested route 
概念為：以Route結構所包裝的另外一個Route結構
具體為：一個Route 元件所包含的另外一個Route 元件


###  nested route 會有的形式會是


1. nested route直接被一個Route元件包覆
```
<Route path='/welcome'>
    <Route path='/welcome/hi'>
        <p>hi</p>
    </Route>
</Route>
```

2. nested route先合併在特定元件上，然後其元件再由Route元件包覆
```
<Route path='/welcome'>
  <Weclome />
</Route>
```

```
function Welcome(props) {
	return (
		<Route path='/welcome/hi'>
	        <p>hi</p>
	    </Route>
	)
}
```

#### 不論是哪一種，其nested route所設定的path只能是？

不論是哪一種，其nested route所設定的path只能是基於包含它的route所設定的path，比如：
在這擁有path2的Route會是nested route，但它的path只能夠以包含它的route所設定的path為主，也就是以\/path1為主，為此nested route的path必須設定為\/path1\/path2才能生效
```
<Route path=/path1>
    <Route path=/path1/path2>
        <p>hi</p>
    </Route>
</Route>
```


##### 若nested route所設定的path設定成以外的path呢？

會因為沒在包含其route所擁有的path而失效



### nested route先合併在特定元件上，然後其元件再由Route元件包覆

若Component 被另一個Route包覆的話，且Component夾雜著Route，那麼該Route那麼就構成nested route，當客戶端要求轉換URL為/path2/path3時，會先從path2對應的Component 進行渲染，然後再從那找到夾雜的Route且Route滿足於/path2/path3，找到後就便渲染對應的component，也就是Component2

```
<Route path=/path2 >
	<Component />
</Route>
```

```
function Component() {
	return (
		<Route path=/path2/path3>
			<Component2 />
		</Route>
	)
}
```

#### 以下面為例

當客戶端要求轉換URL為/welcome/hi時，會先從\/welcome對應的Welcome元件，然後再從Welcome元件設定的Route設定來找到\/hi路徑，並渲染\<p\>hi\<\/p\>

```
function App() {
  return (
    <div>
      <MainHeader />
      <Switch>
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
}
```

```
import { Route } from 'react-router-dom';
const Welcome = (props) => {
  return (
    <div>
      <h2>Welcome page!!!</h2>
      <Route path='/welcome/hi'>
        <p>hi</p>
      </Route>
    </div>
  );
};

export default Welcome;
```


### nest 命名緣由

[[@WhatNest]]
> **Nesting** is a term used to describe the placement of one or more objects within another object.

nest
> to build a nest, or live in a nest
![](https://www.computerhope.com/jargon/n/nest.jpg)

重點：
- nest 動詞是指建立一個特定結構體來包含特定事物

#### nested function

> With computer programming, a nested function is a function contained inside of another function in the source code of a program. An example of this in JavaScript is shown below.


```
function outerFunction() {  
  function innerFunction() {  
    // code  
  }  
}
```

重點：
- nested function：會是指被另一個函式所包含著的函式，舉例來說：innerFunction正是nested function。
```
function outerFunction() {  
  function innerFunction() {  
    // code  
  }  
}
```

## 複習


#🧠 nest 命名緣由在動詞上是什麼意思？ ->->-> `建立一個特定結構體來包含特定事物`
<!--SR:!2023-05-26,106,228-->

#🧠 nested function 是什麼？ ->->-> `是指被另一個函式所包含著的函式`
<!--SR:!2023-09-22,197,248-->

#🧠  nested function：會是指被另一個函式所包含著的函式function outerFunction() \{  function innerFunction() \{  \} } 哪個才是nested function？為什麼？->->-> `innerFunction正是nested function。`
<!--SR:!2023-04-10,97,248-->

#🧠 nested route 概念是什麼？->->-> `以Route結構所包裝的另外一個Route結構`
<!--SR:!2023-04-17,99,248-->

#🧠 nested route 概念為：以Route結構所包裝的另外一個Route結構，具體在React會是什麼元件，請完整說出來 ->->-> `一個Route 元件所包含的另外一個Route 元件`
<!--SR:!2023-05-22,44,208-->


#🧠 react-router-dom v5：每個Route元件對於Router元件是什麼關係？如何定義哪個Route是屬於哪個Router ->->-> `會依據著Route會挑選最近的parent Router來決定其Router的Routing功能`
<!--SR:!2023-10-09,194,230-->

#🧠 react-router-dom v5：nested route 會有的形式會是？->->-> `nested route直接被一個Route元件包覆、nested route先合併在特定元件上，然後其元件再由Route元件包覆`
<!--SR:!2023-09-09,194,250-->


#🧠 react-router-dom v5：nested route 會有的形式會是？若是nested route直接被一個Route元件包覆，那麼會是什麼形式？用程式碼表示->->-> `觀看**nested route 會有的形式會是**章節`
<!--SR:!2023-09-23,197,248-->


#🧠 react-router-dom v5：nested route 會有的形式會是？若是nested route先合併在特定元件上，然後其元件再由Route元件包覆，那麼會是什麼形式？用程式碼表示- ->->-> `觀看**nested route 會有的形式會是**章節`
<!--SR:!2023-05-17,48,228-->


#🧠 react-router-dom v5：nested route 會有的形式會是？若是nested route先合併在特定元件上，然後其元件再由Route元件包覆， 其nested route所設定的path只能是->->-> `不論是哪一種，其nested route所設定的path只能是基於包含它的route所設定的path`
<!--SR:!2023-05-02,112,248-->

#🧠 react-router-dom v5：nested route 會有的形式會是？nested route直接被一個Route元件包覆， 其nested route所設定的path只能是 ->->-> `不論是哪一種，其nested route所設定的path只能是基於包含它的route所設定的path`
<!--SR:!2023-10-28,216,248-->

#🧠 react-router-dom v5：在這擁有path2的Route會是nested route，那麼該Route會是以什麼路徑為主？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667487317/blog/react/react-router/Nested-route/nested-route-example_jcwisx.png)->->-> `但它的path只能夠以包含它的route所設定的path為主，也就是以\/path1為主，為此nested route的path必須設定為\/path1\/path2才能生效`
<!--SR:!2023-12-02,237,248-->

#🧠 react-router-dom v5：不論是哪一種，其nested route所設定的path只能是基於包含它的route所設定的path，若nested route所設定的path設定成以外的path呢？ ->->-> `會因為沒在包含其route所擁有的path而失效`
<!--SR:!2023-09-21,197,248-->

#🧠 react-router-dom v5：若Component 被另一個Route包覆的話，且Component夾雜著Route，那麼該Route那麼就構成nested route，當客戶端要求轉換URL為/path2/path3時，Router會做出什麼反應？說明一下![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667487832/blog/react/react-router/Nested-route/nested-route-inside-component-example1_esnksv.png) ->->-> `若Component 被另一個Route包覆的話，且Component夾雜著Route，那麼該Route那麼就構成nested route，當客戶端要求轉換URL為/path2/path3時，會先從path2對應的Component 進行渲染，然後再從那找到夾雜的Route且Route滿足於/path2/path3，找到後就便渲染對應的component，也就是Component2`
<!--SR:!2023-05-07,113,248-->


#🧠  react-router-dom v5：當客戶端要求轉換URL為/welcome/hi時，Router會做出什麼反應？說明一下![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667487833/blog/react/react-router/Nested-route/nested-route-inside-component-example2_tgbsal.png) ->->-> `當客戶端要求轉換URL為/welcome/hi時，會先從/welcome對應的Welcome元件，然後再從Welcome元件設定的Route設定試著比對，結果目前路徑並非是/hi，所以不會印出hi，最後會以welcome來呈現`
<!--SR:!2023-04-26,93,246-->
<!--SR:!2023-01-09,42,248-->


#🧠  react-router-dom v5：當客戶端要求轉換URL為/welcome/hi時，Router會做出什麼反應？說明一下![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667487833/blog/react/react-router/Nested-route/nested-route-inside-component-example2_tgbsal.png) ->->-> `當客戶端要求轉換URL為/welcome/hi時，會先從/welcome對應的Welcome元件，然後再從Welcome元件設定的Route設定試著比對，結果目前路徑並非是/hi，所以不會印出hi，最後會以welcome來呈現`
<!--SR:!2023-04-26,93,246-->



#🧠  react-router-dom v5：當客戶端要求轉換URL為/welcome/hi時，Router會做出什麼反應？若第二張圖的Route的path設定為/welcome/hi說明一下![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667487833/blog/react/react-router/Nested-route/nested-route-inside-component-example2_tgbsal.png) ->->-> ``
<!--SR:!2023-06-11,121,246-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router-dom：Router 元件的routing 功能是由Route元件來決定，具體的隸屬關係是Route本身會以最近的parent Router作為定義該Router的Routing功能]]
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References:
[[@WhatNest]]