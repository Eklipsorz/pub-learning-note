## 描述
[[@readfogZhongJavaScriptDeBangDing]]



> ### **01、this 默認綁定**

> this 默認綁定我們可以理解爲函數調用時無任何調用前綴的情景，它無法應對我們後面要介紹的另外四種情況，所以稱之爲默認綁定，默認綁定時 this 指向全局對象（非嚴格模式）：

```
function fn1() {
    let fn2 = function () {
        console.log(this); //window
        fn3();
    };
    console.log(this); //window
    fn2();
};
function fn3() {
    console.log(this); //window
};
fn1();
```

> 這個例子中無論函數聲明在哪，在哪調用，由於函數調用時前面並未指定任何對象，這種情況下 this 指向全局對象 window。


重點：
- default this binding 是指當沒有使用任何一個方法來進行this binding就採用的預設方式
- 其方式為：
	- 若執行環境(Exection Context)下是處於非嚴格模式，this 會被設定成 global object，瀏覽器中會是指window，nodejs則是指global
	- 若執行環境(Exection Context)下是處於嚴格模式，this 會被設定成undefined


#### 案例1
```
function foo() {
	console.log(this.a);
}

var a = 2;

foo()
```

首先當foo執行時，會先依序以下面方式來嘗試確定foo裡頭的this是什麼
	- explicit binding 
	- implicit binding
	- default binding 

結果最後是以default binding 來確定this會指向為global object



### 處於嚴格模式

> 但需要注意的是，在嚴格模式環境中，默認綁定的 this 指向 undefined，來看個對比例子：
```
function fn() {
    console.log(this); //window
    console.log(this.name);
};
function fn1() {
    "use strict";
    console.log(this); //undefined
    console.log(this.name);
};
var name = '聽風是風';
fn(); 
fn1() //TypeError: Cannot read property 'a' of undefined
```

> 再例如函數以及調用都暴露在嚴格模式中的例子：
```
"use strict";
var name = '聽風是風';
function fn() {
    console.log(this); 
    console.log(this.name);
};
fn();
```

>最後一點，如果在嚴格模式下調用不在嚴格模式中的函數，並不會影響 this 指向，來看最後一個例子：
```
var name = '聽風是風';
function fn() {
    console.log(this); 
    console.log(this.name); 
};
(function () {
    "use strict";
    fn();
}());
```

重點：
- 若目前執行環境或者全域環境下設定成嚴格模式，就會讓default binding 改指向為undefined
- 若目前執行環境下沒設定嚴格模式或者沒在全域環境下設定嚴格模式，就會讓default binding 改指向為global object

#### 例子1：



若目前執行環境下沒設定嚴格模式，就會讓default binding 改指向為global object
```
var name = '聽風是風';
function fn() {
    console.log(this); //window
    console.log(this.name); //聽風是風
};
(function () {
    "use strict";
    fn();
}());
```

## 複習

#🧠 JS：default this binding  會是什麼？->->-> `指當沒有使用任何一個方法來進行this binding就採用的預設方式`
<!--SR:!2023-09-03,200,248-->

#🧠 JS：default this binding 指當沒有使用任何一個方法來進行this binding就採用的預設方式， 請問default this binding  具體方式為何 ？ ->->-> `會根據執行環境是否處於嚴格模式來將this設定成global 或者 undefined`
<!--SR:!2023-10-11,205,228-->


#🧠 JS：default this binding  方式為何？若執行環境(Exection Context)下是處於非嚴格模式 ->->-> `this 會被設定成 global object，瀏覽器中會是指window，nodejs則是指global`
<!--SR:!2025-01-03,491,248-->

#🧠 JS：default this binding  方式為何？若執行環境(Exection Context)下是處於嚴格模式 ->->-> `this 會被設定成undefined`
<!--SR:!2024-08-24,415,250-->

#🧠 執行以下JS程式碼後，其console會印出什麼？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665409945/blog/javascript/this-binding/default-this-binding-example1_xcvvzd.png) ->->-> `會印出2。 首先當foo執行時，會先依序以下面方式來嘗試確定foo裡頭的this是什麼 - explicit binding  - implicit binding - default binding 。結果最後是以default binding 來確定this會指向為global object`
<!--SR:!2023-09-19,209,248-->


#🧠 若目前執行環境或者全域環境下設定成嚴格模式，default this binding 會變成如何設定？ ->->-> `就會讓default binding 改指向為undefined`
<!--SR:!2023-09-02,200,248-->

#🧠 default this binding 處於何種情況下才會將this設定成undefined? ->->-> `若目前執行環境或者全域環境下設定成嚴格模式`
<!--SR:!2023-11-01,232,248-->

#🧠 若目前執行環境下沒設定嚴格模式或者沒在全域環境下設定嚴格模式，default this binding 會變成如何設定？ ->->-> `就會讓default binding 改指向為global object`
<!--SR:!2023-09-09,201,248-->

#🧠 default this binding 處於何種情況下才會將this設定成global object?  ->->-> `若目前執行環境下沒設定嚴格模式或者沒在全域環境下設定嚴格模式`
<!--SR:!2024-12-19,488,250-->

#🧠 執行以下JS程式碼後，其console會印出什麼？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665410534/blog/javascript/this-binding/strict-default-this-binding-example1_rqracf.png) ->->-> `會印出undefined和報錯，因為處於嚴格模式下的default this binding，會預設將this導向至undefined`
<!--SR:!2023-11-13,206,210-->

#🧠 執行以下JS程式碼後，其console會印出什麼？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665410534/blog/javascript/this-binding/strict-default-this-binding-example2_fa4qff.png) ->->-> `會印出global object的資訊。這是因為目前執行環境或者全域執行環境沒設定嚴格模式，這使得default this binding會直接將this設定為global object`
<!--SR:!2023-12-16,163,228-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置]]
References:
[[@readfogZhongJavaScriptDeBangDing]]