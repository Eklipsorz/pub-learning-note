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
	- forEach 對應的函式並不是以async 和await 來搭配，這使得在for迴圈中執行著擁有promise的callback，會呈現著每一次迭代都產生一個非同步任務，最後由迭代會比這些產生出來的非同步任務還快結束，可能會讓整體模組已經結束執行，而強制結束非同步任務執行，或者同步任務執行完畢，就等非同步任務執行完畢才終止整體模組的執行
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

### 舉例

在這裡會以五次迭代的迴圈來產出五個非同步任務，每個非同步任務會產生一個對於redis資料庫的查詢和關閉資料庫連線
```
const Redis = require('ioredis')
const redisClient = new Redis()

function test() {
	for (let i = 0; i < 5; i++) {
		console.log(redisClient.get("key1"))
		console.log(i)
	}

	redisClient.disconnect()
}

test()

console.log('end')
```

會由於同步任務比產生出來的非同步任務還快執行完畢，所以會先印出還未執行完畢的非同步任務之結果，最後執行到disconnect指令就強制中斷這些非同步任務，而跑出以下結果：
```
Promise { <pending> }
0
Promise { <pending> }
1
Promise { <pending> }
2
Promise { <pending> }
3
Promise { <pending> }
4
end
```
以及一個錯誤訊息表明在對資料庫查詢的時候被迫中斷
```
Error: Connection is closed.
```
### 解法：
1. 在一個以async function內容建立對應await promise就能使同步任務等待非同步任務完成才繼續，以上述例子來說明
```
const Redis = require('ioredis')
const redisClient = new Redis()

async function test() {
	for (let i = 0; i < 5; i++) {
		// 生成非同步，並使for-loop等待
		console.log(await redisClient.get("key1"))
		// 若上面非同步執行還未執行完畢就不執行，執行完畢就繼續執行
		console.log(i)
	}

	redisClient.disconnect()
}

test()

console.log('end')
```

結果會是：
```
end
value1
0
value1
1
value1
2
value1
3
value1
4
```
2. 改寫可支援promise的forEach功能


### 總結
1. 若單純使用for-loop、forEach等沒用async和await包裝的函式執行會使得非同步任務會因同步任務提前結束而出現預期外的錯誤
2. 解法：
	- 使用async/await來包裝
	- 改寫另一個可支援promise的forEach功能：async/await重新包裝



## 複習
#🧠 原生forEach 的callback支不支援promise為主的callback？ 為什麼？（請舉出對應代碼)->->-> `不支援，由於forEach本身並不是async function，且呼叫的callback也不是以await為主`

#🧠 這是JavaScript程式碼，請問非同步任務和同步任務會如何執行？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655196893/blog/promise/synctask-promise_woeyvm.png) ->->-> `迭代(同步任務)會比這些產生出來的非同步任務還快結束，可能會讓整體模組已經結束執行，而強制結束非同步任務執行，或者同步任務執行完畢，就等非同步任務執行完畢才終止整體模組的執行，而這會使得同步任務執行到disconnect，而讓處於資料庫查詢的非同步任務被迫結束而報錯`


#🧠  這是JavaScript程式碼，請問非同步任務和同步任務會如何執行？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655196893/blog/promise/asynctask-promise_sm80it.png) ->->-> `由於添加了async和await，這使得內部的同步任務會等待著產生出來的非同步任務執行完畢才執行下一行。因此每一次迭代會生出非同步任務以及非同步任務執行完畢才會輪到下一個迭代，直到所有迭代完畢，就執行disconnect，此時沒非同步任務，所以可以安全地中斷連線`

#🧠 如何解決原生forEach 的callback不支援promise為主的callback？->->-> `撰寫另一個可支援promise為主的forEach(async/await)或者以async/await來包裝同步任務的for-loop和非同步任務就能達成同樣效果`

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
https://medium.com/@steven234/%E9%81%87%E5%88%B0-async-%E5%88%A5%E7%94%A8-foreach-7cea84f4242f
[[@pangchaWeiShiMejsLiShiYongLiaoawaitDeFangFaBiXuDingYiChengasyncDeZhiHu]]