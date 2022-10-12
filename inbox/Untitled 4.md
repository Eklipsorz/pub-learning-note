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

#### 案例2


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


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@readfogZhongJavaScriptDeBangDing]]