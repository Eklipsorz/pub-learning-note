
## 描述

### Promises chaining


由於Promise API本身具有以下特點：
> 1. Promise 的 then 皆會回傳 Promise object
> 2. 無論你從then呼叫的callback回傳了什麼值，都會自動被設定成鏈串中的下個Promise之fulfillment所擁有的引數


Promise chain 是以then、catch等API將多個Promise串聯起來的非同步任務結構，其結構會依據主要Promise object的處理結果來進行一系列的後續處理

致使可以藉由Promise本身和Promise API提供的then方法，來打造Promise Chain，而這個Chain專門依據特定Promise object的處理結果來進行後續處理，比如：
- Promise 包裝的任務完成後，就會回傳另一個Promise object1
- 第一個then會以回傳後的Promise object1來呼叫執行then以及對應callback：解開Promise object包裝的結果值作為callback的引數來處理，接著回傳另一個Promise object2
- 第二個then會以回傳後的Promise object2來呼叫執行then以及對應callback
- 後續依此類推
```
Promise()
.then(callback1);
.then(callback2);
.then(callback3);
.
.
.then(callbackN);
```

### 若chain中出現錯誤或者rejected狀態的promise
[[@PromisePrototypeThen2022]]

> **備註：** 如果有一個或兩個引數被省略，或為非函式（non-functions），則 `then` 將處於遺失 handler(s) 的狀態，但不會產生錯誤。若發起 `then` 之 `Promise` 採取了一個狀態（實現（`fulfillment）`或拒絕（`rejection））`而 `then` 沒有處理它的函式，一個不具有額外 handlers 的新 `Promise` 物件將被建立，單純採取原 `Promise` 其最終狀態。

[[@PromisePrototypeThen]]
> onRejected Optional
		A Function asynchronously called if the Promise is rejected. This function has one parameter, the rejection reason. If it is not a function, it is internally replaced with a thrower function ((x) => { throw x; }) which throws the rejection reason it received.


> 如果你在一個promise上呼叫 then(..)，而你只傳入一個fulfillment handler給它，它就會以一個預設的rejection handler來替補：
```
var p = new Promise( function(resolve, reject) {
	reject('Ooops');
})

var p2 = p.then(
	functioin fulfilled() {
	
	}
	// 如果省略或者傳入任何的非函式值，
	// 就會使用預設的rejection handler
	// function(error) {
	//     throw err;
	// }
)
```
> 如你所見，預設的rejection handler 單純只會重新植出那個錯誤，最後迫使p2(鏈串的promise)因為同樣的錯誤而被拒絕。基本上，這讓錯誤能夠持續在一個promise串鏈中傳播，直到遭遇明確定義的rejection handler為止

重點：
- 若Promsie chain中的任一個Promise中拋出錯誤而構成rejected promise就會依據當前所在Promise來遍歷後續的chain結構，直到找到對應的rejection handler。
- 其目的在於將接收到的Promise object轉遞到promise chain的後續部分
- 具體實現則是依據著：
	- then 若本身沒設定rejection handler，就會以預設的rejection handler來處理：解開接收到的rejected promise所夾雜的錯誤資訊，然後作為引數來拋出錯誤，然後再經過Promise API轉換成另一個rejected Promise 往下傳遞
	```
	// function(error) {
	//     throw err;
	// }
	```
	- 設定專門攔截錯誤的then或者catch接收：解開接收到的rejected promise所夾雜的錯誤資訊，然後作為引數來處理

### 如果then 方法沒有對應的handler

#### 如果then 方法沒有rejection handler
參照 **若chain中出現錯誤或者rejected狀態的promise** 章節所描述的

#### 如果then 方法沒有fuilfillment handler

> 如果沒有有效的函式被傳入作為then(..)的fulfillment handler參數，也會有一個預設的handler來替補


```
var p = Promise.resolve(42);

p.then(
	// 預設的 fulfillment handler，
	// 如果被省略或者被傳入其他的非函式值，就使用下者
	// function(v) {
	//    return v
	// }
	null,
	function rejected(error) {
		//....
	}
)
```

> 如你所見，這個預設的fullfillment handler 單純會把它所接受的任何值往下一個promise傳遞

重點：
- 若Promise API中的then方法並沒有fulfillment handler，那麼就以預設的fulfillment handler來處理：直接將接收到的Promise object，解開其值並重新包裝成fulfilled 狀態的
- 其目的在於將接收到的Promise object轉遞到promise chain的後續部分
- Promise object 的 預設fulfillment handler：
```
	// function(v) {
	//    return v
	// }
```



## 複習
#🧠 Promise API 的 promise chain 是什麼結構 ->->-> `Promise chain 是以then、catch等API將多個Promise串聯起來的非同步任務結構`

#🧠 Promise API 的Promise chain 是以then、catch等API將多個Promise串聯起來的非同步任務結構，用途為何？ ->->-> `定義以主要Promise object的處理結果來進行一系列的後續處理`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 
Tags:
[[JavaScript]] - [[Promise]]
Links:
References:
[[@PromisePrototypeThen2022]]
[[@PromisePrototypeThen]]