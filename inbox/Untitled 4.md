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
    console.log(this); //undefined
    console.log(this.name);//報錯
};
fn();
```

>最後一點，如果在嚴格模式下調用不在嚴格模式中的函數，並不會影響 this 指向，來看最後一個例子：
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


---
Status: #🌱 
Tags:
Links:
References:
[[@readfogZhongJavaScriptDeBangDing]]