## 描述


### nested route 
概念為：以Route結構所包裝的另外一個Route結構
具體為：一個Route 元件所包含的另外一個Route 元件

### Router 下的後裔Route 元件可以在任何頁面出現

由於Router 下的後裔Route 元件可以在任何頁面出現

```
function Component () {
	return (
		<Route path=target />
	)
}
```

### React-router-dom：nested route

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

### 

```
<Route path='/welcome'>
    <Route path='/welcome/hi'>
        <p>hi</p>
    </Route>
</Route>
```


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

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@WhatNest]]