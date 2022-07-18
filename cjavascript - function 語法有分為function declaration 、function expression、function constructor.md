## 描述

> A function expression is very similar to and has almost the same syntax as a function declaration (see function statement for details). The main difference between a function expression and a function declaration is the function name, which can be omitted in function expressions to create anonymous functions.


```
function (param0) {
  statements
}
function (param0, param1) {
  statements
}
function (param0, param1, /* … ,*/ paramN) {
  statements
}

function name(param0) {
  statements
}
function name(param0, param1) {
  statements
}
function name(param0, param1, /* … ,*/ paramN) {
  statements
}
```

重點：
- function expression 在程式語言中是以 由 function 關鍵字和語法 來代表其對應function之回傳值  或者 
- 在JavaScript 中，通常是由function 這關鍵字搭配以下參數來代表其對應function 之回傳值：
	- 函式名稱：可選擇不填入，來當作匿名函式
	- 函式引數(function argument)
	- 函式內部執行語句


### expression  命名緣由 

> an expression is a syntactic entity in a programming language that may be evaluated to determine its value


重點：
- expression 在程式語言可以被解析成特定值、特定物件的語法

### statement 命名緣由

> a statement is a syntactic unit of an imperative programming language that expresses some action to be carried out.

重點：
- statement 主要是執行特定行為且不具代表特定值、特定物件的語句

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]] - [[IIFE]] - 
Links:
References:

