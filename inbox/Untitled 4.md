## 描述


> ES6 的箭頭函數是另類的存在，爲什麼要單獨說呢，這是因爲箭頭函數中的 this 不適用上面介紹的四種綁定規則。

> 準確來說，箭頭函數中沒有 this，箭頭函數的 this 指向取決於外層作用域中的 this，外層作用域或函數的 this 指向誰，箭頭函數中的 this 便指向誰。

> 有點喫軟飯的嫌疑，一點都不硬朗，我們來看個例子：
```
function fn() {
    return () => {
        console.log(this.name);
    };
}
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
let bar = fn.call(obj1); // fn this指向obj1
bar.call(obj2); //聽風是風
```

> 箭頭函式的this binding 取自包含它的範疇(enclosing scope，函式或者全域)
> 讓我們以範例說明箭頭函式的語彙範疇(lexical scope)

```
function foo() {
	// 回傳  
	retrun (a) => {
		console.log(this.a)
	}
}


```

重點：



#### 案例1

```
function fn() {
    return () => {
        console.log(this.name);
    };
}
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
let bar = fn.call(obj1); 
bar.call(obj2); 
```

```
function fn() {
    return () => {
        console.log(this.name);
    };
}
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
let bar = fn.call(obj1); // fn this指向obj1
bar.call(obj2); //聽風是風
```

#### 案例2
> 爲啥我們第一次綁定 this 並返回箭頭函數後，再次改變 this 指向沒生效呢？
> 
> 前面說了，箭頭函數的 this 取決於外層作用域的 this，fn 函數執行時 this 指向了 obj1，所以箭頭函數的 this 也指向 obj1。
> 
> 除此之外，箭頭函數 this 還有一個特性，那就是一旦箭頭函數的 this 綁定成功，也無法被再次修改，有點硬綁定的意思。
> 
> 當然，箭頭函數的 this 也不是真的無法修改，我們知道箭頭函數的 this 就像作用域繼承一樣從上層作用域找，因此我們可以修改外層函數 this 指向達到間接修改箭頭函數 this 的目的。
```
function fn() {
    return () => {
        console.log(this.name);
    };
};
let obj1 = {
    name: '聽風是風'
};
let obj2 = {
    name: '時間跳躍'
};
fn.call(obj1)(); // fn this指向obj1,箭頭函數this也指向obj1
fn.call(obj2)(); //fn this 指向obj2,箭頭函數this也指向obj2
```

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[JS：explicit binding 是相較於implicit binding而言，較為直接且明確告知this是設定什麼]]
[[new binding 是由new operator 主導來建立一個物件並以此物件作為特定函式呼叫的this]]
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
References:
[[@readfogZhongJavaScriptDeBangDing]]