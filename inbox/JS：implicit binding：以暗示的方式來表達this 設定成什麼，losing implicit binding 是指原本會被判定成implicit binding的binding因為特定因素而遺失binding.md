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
- implicit binding：以暗示的方式來表達this 設定成什麼
- 該方式是：當函式A呼叫時，若函式A呼叫前面添加一個物件B參考，系統就會認為物件B擁有函式A並呼叫函式A，此時函式A的this就會是物件B
- 細節1：
	- 若函式A呼叫前有多個物件參考的話，會挑選離函式A呼叫較近的物件來設定this

#### 案例1

```
function fn() {
    console.log(this.name);
};
let obj = {
    name: '聽風是風',
    func: fn
};
obj.func() 
```

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



#### 案例2 

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
obj1.o.func() 
```


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

在這裡obj1呼叫屬性o並呼叫o物件下的func，而func的this會依序來決定
	- explicit binding
	- implicit binding
	- default binding

在這裡沒有explicit binding，反倒可以利用implicit binding下- **若函式A呼叫前有多個物件參考的話，會挑選離函式A呼叫較近的物件來設定this** 來決定fn的this為obj而印出行星飛行




### losing implicit binding

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

重點：
- losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失 原本的binding 
	- 原本的binding會是指的是：
		-  implicit binding的函式A所擁有的this是設定為A，遺失的話，就是設定為B
		-  implicit binding的函式A所擁有的this是設定為A，遺失的話，就是設定為window
- 特定因素：
	- 參數傳遞：implicit binding的函式B以參數傳遞至一個特定函式A並在那呼叫參數，該函式A呼叫函式B的形式會致使函式B的this改變
	- 變數賦值：implicit binding的函式B以參照位置賦值至一個變數，而這個變數呼叫函式B的形式會致使函式B的this改變
	


#### 因素1 ：參數傳遞

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

在這裡由於obj.fn 會被當成參數放進fn呼叫，但其實只是將obj.fn的參照位址丟進fn1的param來讓fn1呼叫它，該fn1的this本身就因為default binding 而綁定成global object，所以就會以global object來呼叫param()


#### 因素2：變數賦值
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

在這裡會是將obj.fn的參照位址儲存在fn1上，並讓沒有用任何物件搭配的fn1來呼叫，這使得系統會直接採用default binding所設定的global object來呼叫fn1

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

在這裡將obj.fn的參照位址儲存在obj1的fn變數上，並讓有用obj1的fn來呼叫，這會使得fn的this變成以obj1為this來呼叫。





### implicit 命名緣由為何

> Something that is implicit is expressed in an indirect way.

重點：
- implicit 表示某項事物是以間接且不明確的形式來表達，通常會以暗示來表達特定事物


## 複習

#🧠 implicit 命名緣由為何 ->->-> `表示某項事物是以間接且不明確的形式來表達，通常會以暗示來表達特定事物`

#🧠 implicit binding 是什麼？->->-> `以暗示的方式來表達this 設定成什麼`

#🧠 implicit binding 決定this的方式是什麼？ ->->-> `當函式A呼叫時，若函式A呼叫前面添加一個物件B參考，系統就會認為物件B擁有函式A並呼叫函式A，此時函式A的this就會是物件B`

#🧠 implicit binding：若函式A呼叫前有多個物件參考的話，會如何決定函式A的this 是什麼？->->-> `會挑選離函式A呼叫較近的物件來設定this`

#🧠 請問這是obj.func呼叫後的執行環境所設定的this會是什麼？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665486965/blog/javascript/this-binding/implicit-this-binding/implicit-binding-example_ts85d3.png) ->->-> `會是設定obj並印出obj的name-聽風是風。主要是在函式呼叫前添加物件參考A，其函式呼叫就會被系統認為物件參考A所擁有的函式並且呼叫函式。`

#🧠 請問這是obj.func呼叫後的執行環境會被系統使用哪個this binding方法？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665486965/blog/javascript/this-binding/implicit-this-binding/implicit-binding-example_ts85d3.png)->->-> `會是以implicit binding。由於沒有出現new binding、explicit binding的跡象，所以改試著以implicit binding來判定，結果因為函式呼叫前面有物件，而這正是implicit binding的識別特徵`

#🧠 請問這是obj.o.func呼叫後的執行環境所設定的this會是什麼？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665486965/blog/javascript/this-binding/implicit-this-binding/multiple-object-implicit-binding-example_v4uktk.png)->->-> `會是設定obj並印出obj的name-行星飛行。在這裡是採用implicit binding，並且由於前面有多個物件參考，所以系統會挑選離呼叫最近的o對應之參照，也就是obj。`

#🧠 請問這是obj.o.func呼叫後的執行環境會被系統使用哪個this binding方法？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665486965/blog/javascript/this-binding/implicit-this-binding/multiple-object-implicit-binding-example_v4uktk.png)->->-> `會是以implicit binding。由於沒有出現new binding、explicit binding的跡象，所以改試著以implicit binding來判定，結果因為函式呼叫前面有物件，而這正是implicit binding的識別特徵`


#🧠 losing implicit binding  是什麼？ ->->-> `是指原本會被判定成implicit binding的binding因為特定因素而遺失binding`

#🧠 losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding，其因素通常是什麼？(簡要說明)->->-> `參數傳遞、變數賦值`

#🧠 losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding，其特定因素之一-參數傳遞會是指什麼？ ->->-> ``

#🧠 Question :: ->->-> ``


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置]]
References:
[[@readfogZhongJavaScriptDeBangDing]]