## 描述

[[@readfogZhongJavaScriptDeBangDing]]
> 我們先介紹前四種 this 綁定規則，那麼問題來了，如果一個函數調用存在多種綁定方法，this 最終指向誰呢？這裏我們直接先上答案，this 綁定優先級爲：


> 顯式綁定 > 隱式綁定 > 默認綁定
>
>new 綁定 > 隱式綁定 > 默認綁定


重點：
- 若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定，在這裡會分成兩個場景：
	- explicit binding + implicit binding + default binding
	- new binding + implicit binding + default binding
- explicit binding + implicit binding + default binding 優先權
	- explicit binding > implicit binding > default binding
- new binding + implicit binding + default binding 優先權
	- new binding > implicit binding > default binding

#### 案例1
[[@readfogZhongJavaScriptDeBangDing]]
> 爲什麼顯式綁定不和 new 綁定比較呢？因爲不存在這種綁定同時生效的情景，如果同時寫這兩種代碼會直接拋錯，所以大家只用記住上面的規律即可。
```
function Fn(){
    this.name = '聽風是風';
};
let obj = {
    name:'行星飛行'
}
let echo = new Fn().call(obj);//報錯 call is not a function
```


```
function Fn(){
    this.name = '聽風是風';
};
let obj = {
    name:'行星飛行'
}
let echo = new Fn().call(obj);
```

#### 案例2
> 那麼我們結合幾個例子來驗證下上面的規律，首先是顯式大於隱式：
```
let obj = {
    name:'行星飛行',
    fn:function () {
        console.log(this.name);
    }
};
obj1 = {
    name:'時間跳躍'
};
obj.fn.call(obj1);
```

```
//顯式>隱式
let obj = {
    name:'行星飛行',
    fn:function () {
        console.log(this.name);
    }
};
obj1 = {
    name:'時間跳躍'
};
obj.fn.call(obj1);// 時間跳躍
```


#### 案例3 
> 其次是 new 綁定大於隱式：
```
obj = {
    name: '時間跳躍',
    fn: function () {
        this.name = '聽風是風';
    }
};
let echo = new obj.fn();
echo.name;
```



```
//new>隱式
obj = {
    name: '時間跳躍',
    fn: function () {
        this.name = '聽風是風';
    }
};
let echo = new obj.fn();
echo.name;//聽風是風
```


## 複習

#🧠 若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定，在這裡會分成兩個場景(每個場景都是由各個binding所組成)，哪兩個？->->-> `	- explicit binding + implicit binding + default binding - new binding + implicit binding + default binding`
<!--SR:!2024-07-14,349,230-->


#🧠 若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定，在這裡會分成兩個場景，在explicit binding + implicit binding + default binding場景下的優先權會是？ ->->-> `explicit binding > implicit binding > default binding`
<!--SR:!2024-08-10,401,250-->

#🧠 若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定，在這裡會分成兩個場景，在new binding + implicit binding + default binding 優先權會是？ ->->-> `new binding > implicit binding > default binding`
<!--SR:!2023-09-23,79,230-->

#🧠 請問函式呼叫的this-binding的結果會是誰當fn的this？為什麼![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665563331/blog/javascript/this-binding/new-binding/explicit-and-implicit-binding-example_laasdh.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665563331/blog/javascript/this-binding/new-binding/explicit-and-implicit-binding-example_laasdh.png) ->->-> `obj1，會印出時間跳躍，在這裡出現了explicit binding和implicit binding，優先權會先以explicit binding為主，因此才選上obj1`
<!--SR:!2024-10-27,454,250-->

#🧠 請問函式呼叫的this-binding的結果會是誰當fn的this？為什麼!![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665563331/blog/javascript/this-binding/new-binding/new-and-implicit-binding-example_vgfvkc.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665563331/blog/javascript/this-binding/new-binding/new-and-implicit-binding-example_vgfvkc.png) ->->-> `在這裡會是new 所建立的物件，印出聽風是風。原因在於在這裡混雜new binding 和implicit binding，根據優先權會先選擇new binding來決定。`
<!--SR:!2025-01-09,499,250-->

#🧠 請問函式呼叫的this-binding的結果會是誰當fn的this？為什麼! ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665563938/blog/javascript/this-binding/new-binding/new-and-explicit-binding-example_tmm8oa.png) ->->-> `會報錯，最主要這裡有new binding和explicit binding，然而程式本身不允許這兩者同時出現，所以會報錯`
<!--SR:!2024-04-26,336,250-->

#🧠 假若implicit this binding 是依據呼叫的物件來決定其this，請問執行以下代碼會得到甚麼? 為什麼? ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1690191858/blog/javascript/this-binding/implicit-this-binding/implicit-this-binding-error-example_brlx2l.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1690191858/blog/javascript/this-binding/implicit-this-binding/implicit-this-binding-error-example_brlx2l.png)->->-> `會得到錯誤，因為implicit this binding是限定於該物件所能夠擁有的方法來決定，而obj1並未存在著callThisExample這個方法，所以會因為不存在而無法呼叫成功`
<!--SR:!2023-09-03,24,247-->

#🧠 implicit this binding 是依據呼叫的物件來決定其函式呼叫的this ，這句話是有前提嗎? ->->-> `錯誤的，是以該物件所能夠擁有的方法來決定，若本來就不存在該方法就無法決定`
<!--SR:!2023-09-05,26,247-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[new binding 是由new operator 主導來建立一個物件並以此物件作為特定函式呼叫的this]]
[[JS：explicit binding 是相較於implicit binding而言，較為直接且明確告知this是設定什麼]]
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
References:
[[@readfogZhongJavaScriptDeBangDing]]