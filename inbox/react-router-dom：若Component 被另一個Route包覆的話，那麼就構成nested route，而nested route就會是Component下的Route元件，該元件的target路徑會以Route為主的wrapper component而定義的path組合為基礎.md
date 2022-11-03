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


### nested route先合併在特定元件上，然後其元件再由Route元件包覆

若Component 被另一個Route包覆的話，那麼就構成nested route，而nested route就會是Component下的Route元件，該元件的target路徑會以Route為主的wrapper component而定義的path組合為基礎，Component的Route也就會以\/path2為根節點，換言之，由Component來控管\/path2下的所有路徑

```
<Route path=/path2 >
	<Component />
</Route>
```

#### 目標頁面所在

在這裡擔任nested route的Route path設定只能是以\/path2為基礎來設定，但Route path本身可以將path設定跳脫\/path2以外的路徑
```
<Route path=/outer-path />
```

但Component只能控管\/path2下的所有路徑，而若設定\/outer\-path會因為不在管轄範圍而失效


##### 舉例

假設在path1呈現的頁面會是設定以下Route，但實際上必須要讓URL切換成/path2才能滿足，然而當切換至那URL，就以/path
```
<Route path=/path2 />
```

### 以下面為例

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
      <Route path='/hi'>
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

#🧠 nested function 是什麼？ ->->-> `是指被另一個函式所包含著的函式`

#🧠  nested function：會是指被另一個函式所包含著的函式function outerFunction() \{  function innerFunction() \{  \} } 哪個才是nested function？為什麼？->->-> `innerFunction正是nested function。`

#🧠 nested route 概念是什麼？->->-> `以Route結構所包裝的另外一個Route結構`

#🧠 nested route 概念為：以Route結構所包裝的另外一個Route結構，具體在React會是什麼 ->->-> `一個Route 元件所包含的另外一個Route 元件`


#🧠 react-router-dom：每個Route元件對於Router元件是什麼關係？如何定義哪個Route是屬於哪個Router ->->-> `Router 下的Route 元件可以在Router後裔元件上出現`

#🧠 react-router-dom：nested route 會有的形式會是？->->-> `nested route直接被一個Route元件包覆、nested route先合併在特定元件上，然後其元件再由Route元件包覆`


#🧠 react-router-dom：nested route 會有的形式會是？若是nested route直接被一個Route元件包覆，那麼會是什麼形式？用程式碼表示->->-> `觀看**nested route 會有的形式會是**章節`


#🧠 react-router-dom：nested route 會有的形式會是？若是nested route先合併在特定元件上，然後其元件再由Route元件包覆，那麼會是什麼形式？用程式碼表示- ->->-> `觀看**nested route 會有的形式會是**章節`


#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``





---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router-dom：Router 元件的routing 功能是由Route元件來決定，具體的隸屬關係是Route本身會以最近的parent Router作為定義該Router的Routing功能]]
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References:
[[@WhatNest]]