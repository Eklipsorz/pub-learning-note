## 描述

引用**遇到 async，別用 forEach **所描述

> 先看一下 [**_mozilla文件_**](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)上對 forEach的描述:

```
arr.forEach(function callback(currentValue[, index[, array]]) {  
    //your iterator  
}[, thisArg]);
```

> 這是因為 forEach並**_不會_**在乎 **_callback function_**是不是 [**_async functrion_**](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/async_function)(也就是他的 return是不是一個 promise)、也不會等到 promise被 resolve或 reject才執行下一次迴圈。

> 你可以把 forEach想像成是:
```
Array.prototype.forEach = function (callback) {  
    // this represents our array  
    for (let index = 0; index < this.length; index++) {  
        // We call the callback for each entry  
        callback(this[index], index, this);  
    }  
};
```

> 可以看到 function前面沒有 **_async_**、 callback前面也沒有 **_await_**。

> 這樣就算傳入的是一個 async function也沒有用:

```
texts.forEach(async text => {  
    const res = await addSuffix(text);  
    console.log(res);  
})
```

重點：
- forEach 中的callback原始碼會是如下，對於Promise有幾個疑慮：
	- forEach 對應的函式並不是以async 和await 來搭配，這使得在for迴圈中執行著擁有promise的callback，會呈現著每一次迭代都產生一個非同步任務，最後由迭代會比這些產生出來的非同步任務還快結束，可能會讓整體模組已經結束執行，而強制結束非同步任務執行。
	- 若是在callback添加await，肯定會因為forEach本身不是async而跑出錯誤，甚至被迫執行的話，會重演著第一個情況所述的狀況。
```
Array.prototype.forEach = function (callback) {  
    // this represents our array  
    for (let index = 0; index < this.length; index++) {  
        // We call the callback for each entry  
        callback(this[index], index, this);  
    }  
};
```

### 解法：
1. 在一個以async function內容建立


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
https://medium.com/@steven234/%E9%81%87%E5%88%B0-async-%E5%88%A5%E7%94%A8-foreach-7cea84f4242f
[[@pangchaWeiShiMejsLiShiYongLiaoawaitDeFangFaBiXuDingYiChengasyncDeZhiHu]]