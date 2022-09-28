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
>
> Arguments to prepend to arguments provided to the bound function when invoking `func`.

> ### [Return value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind#return_value "Permalink to Return value")
>
> A copy of the given function with the specified `this` value, and initial arguments (if provided).


重點：
- bind 是 function protype的方法
- 主要用途為透過this 和 引數來重新將舊函式轉換成專門以this和引數來處理的函式
- 用法：
	- thisArg：指定物件來綁定在轉換後函式，會是設定新函式的this變數
	- arg1 - argN ：指定引數來綁定在轉換後的函式
	- 回傳值：一個與thisArg 和 arg1-argN相結合的新函式
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

#🧠 JS：function.protype.bind 用途為何？ ->->-> `透過this 和 引數來重新將舊函式轉換成專門以this和引數來處理的函式`

#🧠 JS：function.protype.bind 用法為何？ ->->-> `function.bind(thisArg, arg1, arg2)`

#🧠 JS：function.bind(thisArg, arg1, arg2) 中的thisArg是什麼？ ->->-> `指定物件來綁定在轉換後函式，會是設定新函式的this變數`

#🧠 JS：function.bind(thisArg, arg1, arg2) 中的 arg1 - arg2 是什麼？ ->->-> `指定引數來綁定在轉換後的函式`

#🧠 JS：function.bind(thisArg, arg1, arg2) 回傳什麼？ ->->-> `一個與thisArg 和 arg1-arg2相結合的新函式`


#🧠 JS：function.bind使用場景為何？ ->->-> `替每個元件打造各自的方法`

#🧠 JS：function.bind使用場景為替每個元件打造各自的方法，憑藉什麼？ ->->-> `運用會與其參數結合成新的函式的特性`


---
Status: #🌱 #📓 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnFunctionPrototypeBind]]