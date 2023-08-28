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
- explicit binding 是相較於implicit binding而言，是以較為直接且明確告知this是設定什麼
- 在這裡的explicit  binding會使用 call 、apply、bind 來直接設定this為何
- call 和 apply 設定this並呼叫的方法可以讓函式本身自行根據this為何而決定要執行什麼樣的內容，bind因回傳函式是直接與參數、this寫死，而很難重複選擇其他物件做為this來決定要執行什麼
- 部分JS API會內建explicit binding 方法，如forEach
```
let obj = {
    name: '聽風是風'
};
[1, 2, 3].forEach(function () {
    console.log(this.name);//聽風是風*3
}, obj);
```

#### 案例1：
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
fn(); 
fn.call(obj1); 
fn.apply(obj2); 
fn.bind(obj3)(); 
```

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

在這裡有四種呼叫，分別this不綁定任何this、this綁定obj1、this綁定obj2、this綁定obj3


####  案例 2：指向參數提供的是 null 或者 undefined，那麼 this 將指向全局對象
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
fn.call(undefined);
fn.apply(null); 
fn.bind(undefined)(); 
```

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


#### 
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
- 語法為：
	- function 為要呼叫的函式
	- thisArg為要設定this的物件
	- arg1至argN是原函式需要的參數
```
function.call()
function.call(thisArg)
function.call(thisArg, arg1, /* …, */ argN)
```
#### apply
[[@mdnFunctionPrototypeApply]]

> The **`apply()`** method calls the specified function with a given `this` value, and `arguments` provided as an array

```
apply(thisArg)
apply(thisArg, argsArray)
```


重點：
- function.protype.apply 設定一個明確的物件來設定該函式的this，設定完就直接呼叫
- 語法為：
	- function 為要呼叫的函式
	- thisArg為要設定this的物件
	- arg1至argN是原函式需要的參數，會以陣列來包裹著
```
function.call()
function.call(thisArg)
function.call(thisArg, [arg1, /* …, */ argN])
```
- 細節：
	- arg1 至 argN 所構成的參數陣列會在函式呼叫時，轉換成
	```
	function1.apply(this, [arg1, ..., argN])

	function1(arg1, ... argN)
	```
#### bind
[[bind 是 function protype的方法，主要用途為透過this 和 引數來重新將舊函式轉換成專門以this和引數來處理的函式]]


### call vs. apply vs. bind

> **call、apply 與 bind 有什麼區別？**

> 1.call、apply 與 bind 都用於改變 this 綁定，但 call、apply 在改變 this 指向的同時還會執行函數，而 bind 在改變 this 後是返回一個全新的 boundFunction 綁定函數，這也是爲什麼上方例子中 bind 後還加了一對括號 () 的原因。

> 2.bind 屬於硬綁定，返回的 boundFunction 的 this 指向無法再次通過 bind、apply 或 call 修改；call 與 apply 的綁定只適用當前調用，調用完就沒了，下次要用還得再次綁。

> 3.call 與 apply 功能完全相同，唯一不同的是 call 方法傳遞函數調用形參是以散列形式，而 apply 方法的形參是一個數組。在傳參的情況下，call 的性能要高於 apply，因爲 apply 在執行時還要多一步解析數組。


重點：
- 共同點：call、apply、bind 主要用於設定this是什麼
- 不同點：
	- 設定this之後會做的事情：call、apply 在設定this的同時，並以設定好的this來執行函式、bind則是設定完this就回傳新的函式
	- 設定this之後是否還能重新設定this：bind 屬於hard-binding，其回傳函式的this不能再通過call、apply、bind來修改；call、apply的this 設定只適用於當前呼叫，下次呼叫想使用同個物件當this，就得重新綁定
	- call 和 apply 之間的參數種類：兩者功能相同
		- call 是使用(this, arg1, arg2, arg3,.....)
		- apply 使用陣列(this, \[arg1, arg2, arg3, ....\] )
		- 在單純改變特定函式呼叫的this之場景，call 效能會略高於apply，因為apply還得再執行進一步將陣列轉換成參數，如
		```
		// 轉換前
		function1.apply([arg1, arg2, ..., argN])
		// 轉換後
		function1(arg1, arg2, ... , argN)
		```

#### 案例3：設定this之後是否還能重新設定this 


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
fn.call(obj1); 
fn();
fn.apply(obj2);
fn(); 
let boundFn = fn.bind(obj1);
boundFn.call(obj2);
boundFn.apply(obj2);
boundFn.bind(obj2)();
```


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
fn.call(obj1); //聽風是風
fn(); //行星飛行
fn.apply(obj2); //時間跳躍
fn(); //行星飛行
let boundFn = fn.bind(obj1);//聽風是風
boundFn.call(obj2);//聽風是風
boundFn.apply(obj2);//聽風是風
boundFn.bind(obj2)();//聽風是風
```

#### 案例4 call 與 apply 功能完全相同 呼叫方式

```
let obj = {
    name: '聽風是風'
};
function fn(age,describe) {
    console.log(`我是${this.name},我的年齡是${age}，我非常${describe}!`);
};
fn.call(obj,'26','帥');
fn.apply(obj,['26','帥']);
```


```
let obj = {
    name: '聽風是風'
};
function fn(age,describe) {
    console.log(`我是${this.name},我的年齡是${age}，我非常${describe}!`);
};
fn.call(obj,'26','帥');//我是聽風是風,我的年齡是26，我非常帥
fn.apply(obj,['26','帥']);//我是聽風是風,我的年齡是26，我非常帥
```



###  explicit 命名緣由
> clear and exact

重點：
- explicit 為明確且準確的

## 複習

#🧠  explicit 命名緣由 ->->-> `為明確且準確的`
<!--SR:!2024-10-08,442,250-->

#🧠 explicit binding 是什麼？ ->->-> ` explicit binding 是相較於implicit binding而言，是以較為直接且明確告知this是設定什麼`
<!--SR:!2024-10-30,456,250-->



#🧠 explicit binding是以較為直接且明確告知this是設定什麼，具體是什麼？ ->->-> `在這裡的explicit  binding會使用 call 、apply、bind 來直接設定this為何`
<!--SR:!2024-10-02,436,250-->

#🧠 JS部分API會不會使用explicit binding方法來設定，舉例來說->->-> `forEach`
<!--SR:!2025-01-16,511,250-->

#🧠 function.protype.call() 是什麼？用途是什麼 ->->-> `設定一個明確的物件來設定該函式的this，設定完就直接呼叫`
<!--SR:!2023-11-06,184,230-->

#🧠 function.protype.call() 語法是什麼？ ->->-> `function.call(thisArg, arg1, /* …, */ argN)`
<!--SR:!2024-10-14,447,250-->

#🧠 function.protype.call() 語法是function.call(thisArg, arg1, \/\* …, \*\/ argN)，請問function、thisArg和arg1至argN會是什麼？>->-> `- function 為要呼叫的函式	- thisArg為要設定this的物件 - arg1至argN是原函式需要的參數`

#🧠 function.protype.apply() 是什麼？->->-> `function.protype.apply 設定一個明確的物件來設定該函式的this，設定完就直接呼叫`
<!--SR:!2024-08-17,408,250-->

#🧠 function.protype.apply() 的語法是什麼？ ->->-> `function.call(thisArg, [arg1, /* …, */ argN])`
<!--SR:!2023-08-29,201,250-->

#🧠 function.protype.apply() 的語法是function.apply(thisArg, \[arg1, \/\* …, \*\/ argN\])，其中的function、thisArg和arg1至argN會是什麼？  ->->-> `	- function 為要呼叫的函式 - thisArg為要設定this的物件 - arg1至argN是原函式需要的參數，會以陣列來包裹著`
<!--SR:!2023-08-31,201,250-->


#🧠 function.apply vs. function.call共同點是什麼->->-> `指定this為特定物件並且呼叫對應函式、呼叫完畢之後，下一次還想使用相同的物件作為this，必需重新執行apply、call並指定this`
<!--SR:!2023-11-14,210,230-->


#🧠 function.apply vs. function.call不同點是什麼->->-> `- 參數的不同，apply是使用陣列來包裹函式呼叫所需要的參數；call則是用a, b, c, d來呼叫 - call 效能會略高於apply，因為apply還得再執行進一步將陣列轉換成參數`
<!--SR:!2024-10-29,456,250-->

#🧠 function.apply 為啥會比function.call還耗一點成本？ ->->-> `最主要要將陣列轉換成參數來呼叫，如function1.apply([arg1, arg2, ..., argN])->function1(arg1, arg2, ... , argN)`
<!--SR:!2024-12-12,483,250-->

#🧠 JS：call、apply、bind 共同點是什麼？ ->->-> `call、apply、bind 主要用於設定this是什麼`
<!--SR:!2024-07-12,381,250-->

#🧠 JS：call、apply、bind 不同點是什麼？  ->->-> `	- 設定this之後會做的事情：call、apply 在設定this的同時，並以設定好的this來執行函式、bind則是設定完this就回傳新的函式 - 設定this之後是否重新設定this：bind 屬於hard-binding，其回傳函式的this不能再通過call、apply、bind來修改；call、apply的this 設定只適用於當前呼叫，下次呼叫想使用同個物件當this，就得重新綁定`
<!--SR:!2024-07-28,390,250-->

#🧠 以下程式碼的呼叫，所擁有this會是什麼以及印出什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665540282/blog/javascript/this-binding/explicit-binding/explicit-binding-example_u5m3ld.png)->->-> `第一個為global object，會印出行星飛行、第二個為obj1，會印出聽風是風、第三個為obj2，會印出時間跳躍、第四個為obj3，會印出echo`
<!--SR:!2024-10-11,445,250-->

#🧠  JS：call 、 apply這兩者和this之間可以做什麼應用？  ->->-> `call 和 apply 設定this並呼叫的方法可以讓函式本身自行根據this為何而決定要執行什麼樣的內容`
<!--SR:!2023-11-25,93,190-->


#🧠 為什麼fn.bind需要多一個括號？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665540282/blog/javascript/this-binding/explicit-binding/explicit-binding-example_u5m3ld.png) ->->-> `因為bind會是回傳一個新的函式物件，要執行裡頭的內容，必需要多一個括號`
<!--SR:!2024-10-12,446,250-->

#🧠 請問下面三個函式呼叫會是得到什麼this以及印出什麼？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665541020/blog/javascript/this-binding/explicit-binding/this-is-window-explicit-binding-example_ozqxrj.png)->->-> `this都為global object，而印出則是印出行星飛行，這是因為如果this設定為null或者undefined，那麼this就指向global object`
<!--SR:!2024-03-07,251,230-->


#🧠 JS：bind所產生出來的新函式所擁有this為A，若經過call或者apply而將this更改成B，請問bind產生出來的新函式所擁有的this會是什麼？為什麼？->->-> `會是A，由於bind新函式的this會直接與當初設定的this綁死，無論事後以call或者apply來更改其this，都無法更改`
<!--SR:!2024-10-10,444,250-->

#🧠 function1.apply(this, \[arg1, ..., argN\]) 在JS的函式呼叫上會被看作是什麼？ ->->-> `function1(arg1, ... argN)`
<!--SR:!2024-08-16,407,250-->

#🧠 以下程式碼的呼叫，所擁有this會是什麼以及印出什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665541826/blog/javascript/this-binding/explicit-binding/explicit-binding-function-call_xgowfl.png) ->->-> `第一個會是obj1，會印出聽風是風、第二個會是global object，會印出行星飛行、第三個會是obj2，會印出時間跳躍、第四個會是global object，會印出行星飛行、第五至第八都會是obj1，會印出聽風是風`
<!--SR:!2023-08-28,199,250-->



#🧠 為什麼第六至第八的呼叫會是obj1當this，並且印出聽風是風？而不是obj2當this，並且印出時間跳躍![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665541827/blog/javascript/this-binding/explicit-binding/explicit-binding-function-call-result_chx2cg.png) ->->-> `最主要是這些都源自於第五個函式所產生出來的新函式，這個新函式已經被綁死在obj1，所以即使事後對新函式做call、apply、bind都無法更改其this。`
<!--SR:!2024-12-11,482,250-->


#🧠 以下程式碼的呼叫，所擁有this會是什麼以及印出什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665543322/blog/javascript/this-binding/explicit-binding/call-apply-in-explicit-binding-example_deppqe.png)->->-> `this皆為this，會印出我是聽風是風,我的年齡是26，我非常帥`
<!--SR:!2025-01-10,500,250-->

#🧠 為什麼fn.apply的陣列可以像fn.call正常印出 **我是聽風是風,我的年齡是26，我非常帥** ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665543322/blog/javascript/this-binding/explicit-binding/call-apply-in-explicit-binding-result_q2jsdb.png)->->-> `因為apply會將陣列自動轉換成('26','帥')來呼叫fn`
<!--SR:!2024-12-28,501,250-->




---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
[[JS：default this binding 是指當沒有使用任何一個方法來進行this binding就採用的預設方式]]
[[call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置]]
References:
[[@readfogZhongJavaScriptDeBangDing]]
[[@mdnFunctionPrototypeCall]]
[[@mdnFunctionPrototypeApply]]
[[@mdnFunctionPrototypeBind]]