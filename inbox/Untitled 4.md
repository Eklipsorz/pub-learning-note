## 描述

### explicit binding 
> ### **03、this 顯式綁定**

> 顯式綁定是指我們通過 call、apply 以及 bind 方法改變 this 的行爲，相比隱式綁定，我們能清楚的感知 this 指向變化過程。來看個例子：
```
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
let obj3 = {
    name: 'echo'
}
var name = '行星飛行';
function fn() {
    console.log(this.name);
};
fn(); //行星飛行
fn.call(obj1); //聽風是風
fn.apply(obj2); //時間跳躍
fn.bind(obj3)(); //echo
```

> 比如在上述代碼中，我們分別通過 call、apply、bind 改變了函數 fn 的 this 指向。

> 在 js 中，當我們調用一個函數時，我們習慣稱之爲函數調用，函數處於一個被動的狀態；而 call 與 apply 讓函數從被動變主動，函數能主動選擇自己的上下文，所以這種寫法我們又稱之爲函數應用。

> 注意，如果在使用 call 之類的方法改變 this 指向時，指向參數提供的是 null 或者 undefined，那麼 this 將指向全局對象。
```
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
var name = '行星飛行';
function fn() {
    console.log(this.name);
};
fn.call(undefined); //行星飛行
fn.apply(null); //行星飛行
fn.bind(undefined)(); //行星飛行
```

>另外，在 js API 中部分方法也內置了顯式綁定，以 forEach 爲例：
```
let obj = {
    name: '聽風是風'
};
[1, 2, 3].forEach(function () {
    console.log(this.name);//聽風是風*3
}, obj);
```

重點：
- explicit binding 是相較於implicit binding而言，較為直接且明確告知this是設定什麼
- 在這裡的implicit 會使用 call 、apply、bind 來直接設定this為何

#### call

call 
[[@mdnFunctionPrototypeCall]]
> The **`call()`** method calls the function with a given `this` value and arguments provided individually.

```
call()
call(thisArg)
call(thisArg, arg1, /* …, */ argN)
```

重點：
- function.protype.call 設定一個明確的物件來設定該函式的this，設定完就直接呼叫

#### apply




### call vs. apply vs. bind




> **call、apply 與 bind 有什麼區別？**

> 1.call、apply 與 bind 都用於改變 this 綁定，但 call、apply 在改變 this 指向的同時還會執行函數，而 bind 在改變 this 後是返回一個全新的 boundFunction 綁定函數，這也是爲什麼上方例子中 bind 後還加了一對括號 () 的原因。

> 2.bind 屬於硬綁定，返回的 boundFunction 的 this 指向無法再次通過 bind、apply 或 call 修改；call 與 apply 的綁定只適用當前調用，調用完就沒了，下次要用還得再次綁。

> 3.call 與 apply 功能完全相同，唯一不同的是 call 方法傳遞函數調用形參是以散列形式，而 apply 方法的形參是一個數組。在傳參的情況下，call 的性能要高於 apply，因爲 apply 在執行時還要多一步解析數組。


重點：
- 共同點：call、apply、bind 主要用於設定this是什麼？
- 不同點：
	- 設定this之後會做的事情：call、apply 在設定this的同時，並以設定好的this來執行函式、bind則是設定完this就回傳新的函式
	- 設定this之後是否重新設定this：bind 屬於hardcoded，其回傳的函式不夠再通過call、apply、bind來修改；call、apply的this 設定只適用於當前呼叫，下次呼叫想使用同個物件當this，就得重新綁定
	- call 和 apply 之間的參數                                                       


###  explicit 命名緣由
> clear and exact

重點：
- explicit 為明確且準確的

## 複習


---
Status: #🌱 #📝 
Tags:
[[JavaScript]]
Links:
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
[[JS：default this binding 是指當沒有使用任何一個方法來進行this binding就採用的預設方式]]
[[由於this binding 會藉由scope chain 來找到，為此必須要先知道call stack 和 call site，才能理解this是隸屬於哪個Execution Context 的this，call site 會是指特定函式被呼叫的位置]]
References:
[[@readfogZhongJavaScriptDeBangDing]]
[[@mdnFunctionPrototypeCall]]