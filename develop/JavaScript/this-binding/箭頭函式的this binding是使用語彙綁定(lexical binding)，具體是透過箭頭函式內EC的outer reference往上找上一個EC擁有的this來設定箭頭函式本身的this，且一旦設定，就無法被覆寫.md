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
	// 回傳一個箭頭函式
	retrun (a) => {
		// 在此，this是從語彙上繼承自foo
		console.log(this.a)
	}
}

var obj1 = {
	a: 2
}

var obj1 = {
	a: 3
}

var bar = foo.call(obj1)
bar.call(obj2) // 2
```

> 在foo()中建立的箭頭函式被呼叫時會從語彙上(lexically) 捕捉 foo() 的this (不管那是什麼)，既然foo()的this 綁定到obj1，bar(對所回傳的箭頭函式的一個參考)的this也會綁定到obj1。箭頭函式的這種語彙綁定(lexical binding)無法被覆寫(即便使用new也一樣)。

> 最常見的使用情況下很可能是用於callback，比如事件處理器(event handlers) 或者 計時器(timers)：

```
function foo() {
	setTimeout(()=>{
		// 這裡this在語彙上繼承自foo
		console.log(this.a)
	}, 100)
}


var obj = {
	a: 2
}

foo.call(obj) // 2
```

> 雖然箭頭函式提供一種替代方式，讓我們不必在一個函式上使用bind(...)來確保this值，這看起來很吸引人，但要注意的重點是，他們基本上使得傳統的this機制失效了，而改用較廣泛被理解的語彙範疇(lexical scoping)。在ES6 之前，我們已經有一種相當常見的模式來達成這樣的效果，它基本上與ES6箭頭函式的精神無異：

```
function foo() {
	var self = this // 語彙上捕捉了 this
	setTimeout(function () {
		console.log(self.a)
	}, 100)
}

var obj = {
	a: 2
}

foo.call(obj) // 2
```

> 雖然self = this 與箭頭函式兩者看起來都像是不想要使用bind(...)時的好解法，但基本上他們是逃離了this而非理解並擁抱它。


>如果你發現自己寫的是this風格的程式碼，但大多時候或總是如此，你都以語彙的self = this 或者箭頭函式這些花招妨礙this機制，那麼你應該考慮以下任一作法：
> 1. 只使用語彙範疇，忘掉那this風格程式碼的假象
>2. 完全擁抱this風格的機制，包括了在必要時使用bind(...)，並試著避免self=this與箭頭函式這種lexical this的花招



重點：
- 箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫
- 箭頭函式本身並不會依據new binding、implicit binding、explicit binding來決定this binding
- 箭頭函式通常使用場景為：
	- 事件處理器
	- 計時器


#### 案例1

```
function foo() {
  const fn = () => {
    return console.log(this.a);
  };

  return fn;
}

var obj1 = {
  a: 2,
};

var obj2 = {
  a: 3,
};

var bar = foo.call(obj1)
bar.call(obj2) 
```

```
function foo() {
  // 回傳一個箭頭函式
  const fn = () => {
	// 在此，this是從語彙上繼承自foo
    return console.log(this.a);
  };

  return fn;
}

var obj1 = {
  a: 2,
};

var obj2 = {
  a: 3,
};

var bar = foo.call(obj1)
bar.call(obj2) // 2
```

> 在foo()中建立的箭頭函式被呼叫時會從語彙上(lexically) 捕捉 foo() 的this (不管那是什麼)，既然foo()的this 綁定到obj1，bar(對所回傳的箭頭函式的一個參考)的this也會綁定到obj1。箭頭函式的這種語彙綁定(lexical binding)無法被覆寫(即便使用new也一樣)。

#### 案例2

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
fn.call(obj1)(); 
fn.call(obj2)(); 
```

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

#### 案例3 

```
function foo() {
	setTimeout(()=>{
		console.log(this.a)
	}, 100)
}


var obj = {
	a: 2
}

foo.call(obj) 
```

```
function foo() {
	setTimeout(()=>{
		// 這裡this在語彙上繼承自foo
		console.log(this.a)
	}, 100)
}


var obj = {
	a: 2
}

foo.call(obj) // 2
```

## 複習

#🧠 箭頭函式的this binding 依據著new binding、implicit binding、explicit binding來決定this binding，這句話是對的嗎->->-> `不是`
<!--SR:!2024-03-21,318,250-->

#🧠 箭頭函式的this binding 和 其他一般函式呼叫的this binding有何不一樣？ ->->-> `箭頭函式是採用語彙綁定，並不會依據著new binding、implicit binding、explicit binding來決定this binding。一般函式呼叫的this binding會是依據著new binding、implicit binding、explicit binding來決定this binding`
<!--SR:!2024-07-25,385,250-->


#🧠 箭頭函式的this binding 一旦經由語彙綁定來決定this，爾後還能更改其this嗎？->->-> `不能`
<!--SR:!2023-12-06,99,230-->


#🧠 箭頭函式的this binding 方式是什麼？ ->->-> `箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫`
<!--SR:!2024-10-13,447,250-->

#🧠 箭頭函式的通常使用場景為 ->->-> `- 事件處理器 - 計時器`
<!--SR:!2023-09-18,74,230-->



#🧠 請問以下函式呼叫的this會是什麼？會印出什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665578883/blog/javascript/this-binding/arrow-function-this-binding/arrow-function-this-binding-example1_zumv9b.png) ->->-> `bar那行會以this為obj1來執行foo並獲得一個函式物件，其函式物件會是因為語彙綁定而綁死obj1，接著bar.call(obj2)不會以obj2為this來印出3，而是以綁死的obj1和2`
<!--SR:!2023-11-22,97,230-->

#🧠 請問以下函式呼叫的this會是什麼？會印出什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665578883/blog/javascript/this-binding/arrow-function-this-binding/arrow-function-this-binding-example2_it4l4s.png) ->->-> `第一行fn會是以obj1當作this來呼叫，而使回傳的函式會因為語彙綁定而綁定在obj1，呼叫時會是以obj1來呼叫並且印出聽風是風；第二行fn會是以obj2當作this來呼叫，而使回傳的函式會因為語彙綁定而綁定在obj2，呼叫時會是以obj2來呼叫並且印出時間跳躍。`
<!--SR:!2024-07-01,375,250-->

#🧠 請問以下函式呼叫的this會是什麼？會印出什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665578883/blog/javascript/this-binding/arrow-function-this-binding/arrow-function-this-binding-example3_s3srqa.png) ->->-> `執行foo.call(obj)，會是以obj為this來呼叫並生成非同步計時任務，此計時任務也會因為語彙綁定往上找this而找上foo的this而設定成obj，並印出2`
<!--SR:!2024-09-26,430,250-->

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