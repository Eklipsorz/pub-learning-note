## 描述

[[@mdnFunctionPrototypeBind]]
> The **`bind()`** method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.


```
bind(thisArg)
bind(thisArg, arg1)
bind(thisArg, arg1, arg2)
bind(thisArg, arg1, arg2, /* …, */ argN)
```

```
function log(...args) {
  "use strict"; // prevent `this` from being boxed into the wrapper object
  console.log(this, ...args);
};
const boundLog = log.bind("this value", 1, 2);
```

> `thisArg`
>
> The value to be passed as the `this` parameter to the target function `func` when the bound function is called

>`arg1, …, argN` Optional

> Arguments to prepend to arguments provided to the bound function when invoking `func`.


重點：
- bind 是 function protype的方法
- 主要用途為透過this 和 引數來重新將舊函式轉換成專門以this和引數來處理的函式
- 用法：
	- thisArg：是要綁定的物件為何，會是設定新函式的
	- 
```
function.bind(thisArg)
function.bind(thisArg, arg1)
function.bind(thisArg, arg1, arg2)
function.bind(thisArg, arg1, arg2, /* …, */ argN)
```


### 使用場景
1. 運用會與其參數結合成新的函式的特性-來替每個元件打造各自的方法，比如每個項目的移除項目功能，舉例來說明，會以remove函式為原型，該函式會以id來移除對應項目，透過bind，可以替每個項目建立各自的移除項目功能，如項目1就擁有item1Remove這函式，它一呼叫就只移除項目1

```
function remove(id) {
	//...
}

const item1Remove = remove.bind(null, id1)
const item2Remove = remove.bind(null, id2)
const item2Remove = remove.bind(null, id3)
```

## 複習


---
Status: #🌱 #📓 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnFunctionPrototypeBind]]