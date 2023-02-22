


### 若chain中出現錯誤或者rejected狀態的promise
[[@PromisePrototypeThen2022]]

> **備註：** 如果有一個或兩個引數被省略，或為非函式（non-functions），則 `then` 將處於遺失 handler(s) 的狀態，但不會產生錯誤。若發起 `then` 之 `Promise` 採取了一個狀態（實現（`fulfillment）`或拒絕（`rejection））`而 `then` 沒有處理它的函式，一個不具有額外 handlers 的新 `Promise` 物件將被建立，單純採取原 `Promise` 其最終狀態。

[[@PromisePrototypeThen]]
> onRejected Optional
		A Function asynchronously called if the Promise is rejected. This function has one parameter, the rejection reason. If it is not a function, it is internally replaced with a thrower function ((x) => { throw x; }) which throws the rejection reason it received.



自動解開rejected狀態的promise所夾雜的錯誤資訊

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

> 如你所見，這個預設的fullfillment handler 單純ㄏㄨ
## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@PromisePrototypeThen2022]]
[[@PromisePrototypeThen]]