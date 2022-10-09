## 描述


### implicit binding

> #### **1）、隱式綁定**

> 什麼是隱式綁定呢，如果函數調用時，前面存在調用它的對象，那麼 this 就會隱式綁定到這個對象上，看個例子：
```
function fn() {
    console.log(this.name);
};
let obj = {
    name: '聽風是風',
    func: fn
};
obj.func() //聽風是風
```

> 如果函數調用前存在多個對象，this 指向距離調用自己最近的對象，比如這樣：
```
function fn() {
    console.log(this.name);
};
let obj = {
    name: '行星飛行',
    func: fn,
};
let obj1 = {
    name: '聽風是風',
    o: obj
};
obj1.o.func() //行星飛行
```

> 那如果我們將 obj 對象的 name 屬性註釋掉，現在輸出什麼呢？
```
function fn() {
    console.log(this.name);
};
let obj = {
    func: fn,
};
let obj1 = {
    name: '聽風是風',
    o: obj
};
obj1.o.func() //？？
```

> 這裏輸出 undefined，大家千萬不要將作用域鏈和原型鏈弄混淆了，obj 對象雖然 obj1 的屬性，但它兩原型鏈並不相同，並不是父子關係，由於 obj 未提供 name 屬性，所以是 undefined。


重點：
- implicti
- 當函式A呼叫時，若函式A呼叫前面添加一個物件B參考，系統就會認為物件B擁有函式A並呼叫函式A


### implicit binding is lost

> #### **2）、隱式丟失**

> 在特定情況下會存在隱式綁定丟失的問題，最常見的就是作爲參數傳遞以及變量賦值，先看參數傳遞：
```
var name = '行星飛行';
let obj = {
    name: '聽風是風',
    fn: function () {
        console.log(this.name);
    }
};
function fn1(param) {
    param();
};
fn1(obj.fn);//行星飛行
```

>這個例子中我們將 obj.fn 也就是一個函數傳遞進 fn1 中執行，這裏只是單純傳遞了一個函數而已，this 並沒有跟函數綁在一起，所以 this 丟失這裏指向了 window。
>
>第二個引起丟失的問題是變量賦值，其實本質上與傳參相同，看這個例子：
```
var name = '行星飛行';
let obj = {
    name: '聽風是風',
    fn: function () {
        console.log(this.name);
    }
};
let fn1 = obj.fn;
fn1(); //行星飛行
```

>注意，隱式綁定丟失並不是都會指向全局對象，比如下面的例子：
```
var name = '行星飛行';
let obj = {
    name: '聽風是風',
    fn: function () {
        console.log(this.name);
    }
};
let obj1 = {
    name: '時間跳躍'
}
obj1.fn = obj.fn;
obj1.fn(); //時間跳躍
```

>雖然丟失了 obj 的隱式綁定，但是在賦值的過程中，又建立了新的隱式綁定，這裏 this 就指向了對象 obj1。

## 複習


---
Status: #🌱 #📝 
Tags:
[[JavaScript]]
Links:
[[由於this binding 會藉由scope chain 來找到，為此必須要先知道call stack 和 call site，才能理解this是隸屬於哪個Execution Context 的this，call site 會是指特定函式被呼叫的位置]]
References:
[[@readfogZhongJavaScriptDeBangDing]]