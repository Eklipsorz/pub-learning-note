## 描述

### arrow function 
箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫

### 案例：arrow function 採用至implicit binding
```
const testhandler = () => {
  console.log(this, this.name);
};
function testhandler2() {
  console.log(this, this.name);
}
var name = 'window';
const object = {
  name: 'object',
  fn: testhandler,
};

object.fn();
```

首先在建立testhandler 所對應函式物件時，由於是箭頭函式，其this 綁定會以建立時的環境來設定，在這裡會因為scope chain而找到全域環境的this來設定成global object，建立箭頭函式為主的函式物件之後，其函式的this會一直固定在global object。

之後不論怎麼改this，都因 **一旦設定，就無法被覆寫** 這特性而無法更改，所以在這裡會印出global object和它的屬性


```
const testhandler = () => {
  console.log(this, this.name);
};

function testhandler2() {
  console.log(this, this.name);
}
var name = 'window';
const object = {
  name: 'object',
  fn: testhandler2,
};

object.fn();
```

若將fn調整成一般函式，其fn的結果會是object和它的屬性


### 案例：arrow function 採用至explicit binding

```
const testhandler = () => {
  console.log(this, this.name);
};

function testhandler2() {
  console.log(this, this.name);
}
var name = 'window';
const object = {
  name: 'object',
};

testhandler.bind(object)();
```

結果會是global和global為主的屬性

```
const testhandler = () => {
  console.log(this, this.name);
};

function testhandler2() {
  console.log(this, this.name);
}
var name = 'window';
const object = {
  name: 'object',
};

testhandler2.bind(object)();
```

結果會是object和object為主的屬性




## 複習

#🧠 請問最後印出的結果是什麼？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668432831/blog/javascript/this-binding/arrow-function-this-binding/example/arrow-function-this-binding-example2-with-implicity-binding_zg1f7h.png) ->->-> `會印出object和object這字串，因為fn會對應到一般函式，會在執行時決定其this`


#🧠 請問最後印出的結果是什麼？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668432831/blog/javascript/this-binding/arrow-function-this-binding/example/arrow-function-this-binding-example1-with-implicity-binding_edoiom.png) ->->-> `首先在建立testhandler 所對應函式物件時，由於是箭頭函式，其this 綁定會以建立時的環境來設定，在這裡會因為scope chain而找到全域環境的this來設定成global object，建立箭頭函式為主的函式物件之後，其函式的this會一直固定在global object。 之後不論怎麼改this，都因 **一旦設定，就無法被覆寫** 這特性而無法更改，所以在這裡會印出global object和它的屬性`


#🧠 arrow function 的this binding 綁定後還能再修改嗎？->->-> `一旦設定，就無法被覆寫`


#🧠  請問最後印出的結果是以global object，而非是object，請問為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668432831/blog/javascript/this-binding/arrow-function-this-binding/example/arrow-function-this-binding-example1-with-implicity-binding_edoiom.png) ->->-> `由於是箭頭函式，其this 綁定會以建立時的環境來設定，在這裡會因為scope chain而找到全域環境的this來設定成global object，建立箭頭函式為主的函式物件之後，其函式的this會一直固定在global object。 之後不論怎麼改this，都因 **一旦設定，就無法被覆寫** 這特性而無法更改`

#🧠 請問最後印出的結果是什麼？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668434243/blog/javascript/this-binding/arrow-function-this-binding/example/arrow-function-this-binding-example1-with-explicit-binding_eubb8t.png) ->->-> `global和global為主的屬性`

#🧠 請問最後印出的結果是什麼？為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668434243/blog/javascript/this-binding/arrow-function-this-binding/example/arrow-function-this-binding-example2-with-explicit-binding_zeya6q.png) ->->-> `object和object為主的屬性`



---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
[[當執行Bytecode來決定this binding時，若是遇到：非箭頭函式呼叫，就分別以new binding、implicit binding、explicit binding、default binding來決定他們函式呼叫時的this 是什麼；箭頭函式呼叫，就以語彙綁定]]
[[箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫]]
References: