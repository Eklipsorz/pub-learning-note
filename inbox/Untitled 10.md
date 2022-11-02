## 描述


### nested route 
概念為：以Route結構所包裝的另外一個Route結構
具體為：一個Route 元件所包含的另外一個Route 元件

### Router 下的後裔Route 元件可以在任何頁面出現

由於Router 下的後裔Route 元件可以在任何頁面出現，

```
function Component 
return (
	<Route path=path1 />
)
```



#### 目標頁面所在

目標頁面所在只能夠是當前頁面所在或者以當前頁面所在為基礎的位置
- /target/path
- /target

目標頁面所在不能跳脫當前頁面所在，因為若設定在當前頁面以外的頁面位置，那就


##### 舉例

假設在path1呈現的頁面會是設定以下Route，但實際上必須要讓URL切換成/path2才能滿足，然而當切換至那URL，就以/path
```
<Route path=/path2 />
```

###

> and if they are on a component which is currently active,  they will evaluated by React Router DOM. if the welcome page is active, this route will be evaluated. if not active, this route will note be evaluated



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


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@WhatNest]]