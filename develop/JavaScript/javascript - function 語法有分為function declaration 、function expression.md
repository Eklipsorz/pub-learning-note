## 描述

### function declaration

[[@mdnFunctionDeclarationJavaScript]] 所描述：
> The **function declaration** (function statement) defines a function with the specified parameters.

重點：
- function declaration 是向系統告知 特定函式的存在 以及 特定識別字對應著存放函式內容的記憶體區塊
- 具體會使用function關鍵字、function名稱、function引數、function裡的語法來宣告函式的存在，並分配記憶體來存放對應函式內容，並讓function名稱去對應

### function expression
[[@mdnFunctionExpressionJavaScript]] 所描述：
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
- function expression 在程式語言中是以 由 function 關鍵字和語法 來代表其對應function之回傳值  或者 以整個函式來表達整個函式
- 在JavaScript 中，通常是由function 這關鍵字搭配以下內容來代表其對應function 之回傳值或者代表整個函式：
	- 函式名稱：可選擇不填入，來當作匿名函式
	- 函式引數(function argument)
	- 函式內部執行語句

### function declaration vs. function expression 


[[@mdnFunctionExpressionJavaScript]] 所描述：

> A function expression is very similar to and has almost the same syntax as a function declaration (see function statement for details). The main difference between a function expression and a function declaration is the function name, which can be omitted in function expressions to create anonymous functions.


重點：
- function declaration 主要是向系統宣告函式存在，function expression則是以表達特定函式/特定物件/特定值的表達式，只是是使用function形式來表達
- function declaration 一定得要有 function 關鍵字、function 名稱、function 引數、function 語句
- function expression 一定得要有 function 關鍵字、函式引數、函式內部執行語句，函式名稱是不一定有

### expression  命名緣由 

> an expression is a syntactic entity in a programming language that may be evaluated to determine its value


重點：
- expression 是一種語法
- 在程式語言可以被解析成特定值、特定物件的語法，換言之，表達其特定值、特定物件的語法
- 若語法本身就是特定值、特定物件，語法也算是expression，如1、2、3

### statement 命名緣由

> a statement is a syntactic unit of an imperative programming language that expresses some action to be carried out.

重點：
- statement 是一種語法
- 主要是執行特定行為且不具代表特定值、特定物件的語法

### declaration 命名緣由

> a declaration is a language construct specifying identifier properties: it declares a word's (identifier's) meaning.

重點：
- declaration 是一種語法
- 主要宣告系統某個識別字對應什麼物件/函式/數值，以此告知其存在

## 複習
#🧠 電腦科學裡的expression是什麼 ->->-> `在程式語言可以被解析成特定值、特定物件的語法，換言之，表達其特定值、特定物件的語法`
<!--SR:!2024-05-30,413,250-->

#🧠 電腦科學裡的語法若本身就是 特定值、特定物件，那麼會可以算是expression？->->-> `可以`
<!--SR:!2024-01-08,124,230-->

#🧠 電腦科學裡的declaration是什麼 ->->-> `主要宣告系統某個識別字對應什麼物件/函式/數值，以此告知其存在`
<!--SR:!2023-12-07,195,230-->

#🧠  電腦科學裡的statement是什麼 ->->-> `主要是執行特定行為且不具代表特定值、特定物件的語法`
<!--SR:!2024-11-11,469,230-->

#🧠 function declaration 是什麼？  ->->-> `function declaration 是向系統告知 特定函式的存在 以及 特定識別字對應著存放函式內容的記憶體區塊`
<!--SR:!2024-02-22,212,230-->

#🧠 具體如何實現function declaration->->-> `具體會使用function關鍵字、function名稱、function引數、function裡的語法來宣告函式的存在，並分配記憶體來存放對應函式內容，並讓function名稱去對應`
<!--SR:!2023-10-31,283,250-->

#🧠 function expression 是什麼？ ->->-> `function expression 在程式語言中是以 由 function 關鍵字和語法 來代表其對應function之回傳值  或者 以整個函式來表達整個函式`
<!--SR:!2024-08-11,458,250-->

#🧠 在JavaScript 中，通常是由function 這關鍵字搭配哪些內容來代表其對應function 之回傳值或者代表整個函式 ->->-> `函式名稱：可選擇不填入，來當作匿名函式、函式引數(function argument)、函式內部執行語句`
<!--SR:!2024-01-03,103,210-->


#🧠 在JavaScript 中，function declaration vs. function expression 差別？(語法&功能上) ->->-> `function declaration 主要是向系統宣告函式存在，function expression則是以表達特定函式/特定物件/特定值的表達式，只是是使用function形式來表達、 function declaration 一定得要有 function 關鍵字、function 名稱、function 引數、function 語句、function expression 一定得要有 function 關鍵字、函式引數、函式內部執行語句，函式名稱是不一定有`
<!--SR:!2023-11-05,102,229-->



---
Status: #🌱 
Tags:
[[JavaScript]] - [[IIFE]] 
Links:
References:
[[@mdnFunctionDeclarationJavaScript]]
[[@mdnFunctionExpressionJavaScript]]