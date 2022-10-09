## 描述


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


> **call、apply 與 bind 有什麼區別？**

> 1.call、apply 與 bind 都用於改變 this 綁定，但 call、apply 在改變 this 指向的同時還會執行函數，而 bind 在改變 this 後是返回一個全新的 boundFunction 綁定函數，這也是爲什麼上方例子中 bind 後還加了一對括號 () 的原因。

> 2.bind 屬於硬綁定，返回的 boundFunction 的 this 指向無法再次通過 bind、apply 或 call 修改；call 與 apply 的綁定只適用當前調用，調用完就沒了，下次要用還得再次綁。

> 3.call 與 apply 功能完全相同，唯一不同的是 call 方法傳遞函數調用形參是以散列形式，而 apply 方法的形參是一個數組。在傳參的情況下，call 的性能要高於 apply，因爲 apply 在執行時還要多一步解析數組。


## 複習


---
Status: #🌱 #📝 
Tags:
[[JavaScript]]
Links:
References: