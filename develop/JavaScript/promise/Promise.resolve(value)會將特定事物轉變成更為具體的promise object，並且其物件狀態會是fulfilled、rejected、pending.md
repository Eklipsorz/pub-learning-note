
## 描述



> 第一個參數就沒那麼容易決定了，它在Promise的相關文獻中常被標示為resolve(..)。這個用詞顯然與 **resolution (解析)** 有關。

> 但如果這個參數看似專門用來履行(fulfill) Promise，為何我們叫它resolve(..)，而不是應該更為正確的fulfill(..)呢？ 為了回答此問題，讓我們也看一下Promise API這兩個方法：
```
var fulfilledPr = Promise.resolve(42);
var rejectedPr = Promise.reject('Oops');
```


> Promise.resolve(..) 創建一個會解析為所給的值的Promise。在這個例子中，42是一個普通的、非Promise、非thenable的值，所以就為42這個值創建了履行的承諾(fulfilled promise) fulfilledPr。Promise.reject('Oops')為'Oops' 這個理由創建了拒絕的承諾(rejected promise) rejectedPr。


> 現在讓我們說明為何 **resolve** 這個用語 (如Promise.resolve(..) 中所用的) 更加清楚也確實更為精確，如果是明確用在可能產生fulfillment 或者rejection 任一者的情境下的話：

```
var rejectedTh = {
	then: function(resolved, rejected) {
		rejected('Oops');
	}
}

var rejectedPr = Promise.resolve(rejectedTh);
```

> 如我們在本章前面討論過的，Promise.resolve(..) 會執行回傳所收到的真正Promise，或是解開收到的thenable。如果那個thenable的解開動作揭露出一個被拒絕的狀態，那麼從Promise.resolve(..)回傳的Promise實際上也會是相同的拒絕狀態。

> 所以Promise.resolve(..)是這個API方法良好且精確的名稱，因為他實際上可能會產生fulfillment或者rejection任一個狀態。

> Promise(..) 建構器的第一個callback參數會解開一個thenable(跟Promise.resolve(..)相同)或一個真正的Promise：

```
var rejectedPr = new Promise( function(resolve, reject) => {
	// 以一個被拒絕的Promise 來解析這個Promise
	resolve(Promise.reject('Oops'));
})

rejectedPr.then (
	function fulfilled() {
		// 永遠到不了這裡
	},
	function rejected(err) {
		console.log(error)
	}
);
```


### 語法

[[@PromiseResolveJavaScript2023]]
> Syntax
		Promise.resolve(value)

> Parameters
		value
			Argument to be resolved by this Promise. Can also be a Promise or a thenable to resolve.


>If a non-thenable value is passed, the returned promise is already fulfilled with that value.
> 
  If a thenable is passed, the returned promise will adopt the state of that thenable by calling the **"then method"** and passing a pair of resolving functions as arguments.


```
// Resolving a thenable object
var p1 = Promise.resolve({
  then: function(onFulfill, onReject) { onFulfill('fulfilled!'); }
});
console.log(p1 instanceof Promise) // true, object casted to a Promise

p1.then(function(v) {
    console.log(v); // "fulfilled!"
  }, function(e) {
    // not called
});

// Thenable throws before callback
// Promise rejects
var thenable = { then: function(resolve) {
  throw new TypeError('Throwing');
  resolve('Resolving');
}};

var p2 = Promise.resolve(thenable);
p2.then(function(v) {
  // not called
}, function(e) {
  console.log(e); // TypeError: Throwing
});

// Thenable throws after callback
// Promise resolves
var thenable = { then: function(resolve) {
  resolve('Resolving');
  throw new TypeError('Throwing');
}};

var p3 = Promise.resolve(thenable);
p3.then(function(v) {
  console.log(v); // "Resolving"
}, function(e) {
  // not called
});
```

重點：
- Promise API 的 resolve 意味著將指定事物轉變成更為具體、清楚的形式，也就是將指定事物轉變成promise object來包裝其事物的結果物件
- resolve 所能得到的形式會是以下任一形式：
	- 具有pending狀態的promise object，其結果值會是無，但僅僅限定於thenable或者正在處於pending狀態的promise object，由於只有經過resolve執行就會以非同步形式來呼叫thenable的then方法，而獲取該promise object若是在call stack還有任務的情況下取得，那麼勢必為pending
	- 具有fulfilled狀態的promise object，其結果值會是原本的指定事物
	- 具有rejected狀態的promise object，其結果值會是原本的指定事物
- 語法為：
	- value 為 非thenable的內容或者不為promise object的話，promise.resolve就會回傳fulfilled狀態的promise object，其結果值會是value
	- value 為thenable的內容，promise.resolve就會回傳pending狀態的promise object。
	- value 為promise object的內容，promise.resolve就會直接回傳該promise object
```
語法1：
promise.resolve(value)

語法2：
new Promise((resolve, _) => {
	// ...
	resolve(value)
})
```




#### resolve 命名緣由

> If you resolve something into a clearer form, or if it resolves into a clearer form, its shape or the different parts it contains become clear.


重點：
- resolve 中文意思為解析
- resolve 會是指將特定事物轉換成更為清楚、更為具體的形式

## 複習

#🧠 resolve 命名緣由為何？ ->->-> `解析、將特定事物轉換成更為清楚、更為具體的形式`
<!--SR:!2024-03-03,223,250-->

#🧠  Promise API 的 resolve 意味著什麼？或者說為何取名為resolve？ ->->-> `意味著將指定事物轉變成更為具體、清楚的形式，也就是將指定事物轉變成promise object來包裝其事物的結果物件`
<!--SR:!2023-12-27,188,250-->

#🧠 Promise API 的 resolve 所能得到的形式會是什麼狀態的promise？ ->->-> `	- 具有pending狀態的promise object，其結果值會是無，但僅僅限定於thenable - 具有fulfilled狀態的promise object，其結果值會是原本的指定事物 - 具有rejected狀態的promise object，其結果值會是原本的指定事物`
<!--SR:!2024-03-16,205,230-->

#🧠 Promise API 的 resolve 所能得到的形式若是具有pending狀態的promise object，那麼其可能性會是什麼？ ->->-> `promise object包裝的任務本身會是非同步任務，該任務目前處於被排程且還未被執行，因此處於pending`
<!--SR:!2024-03-13,233,250-->

#🧠 Promise API 的 resolve(thenable) 所能得到的形式若是具有pending狀態的promise object，那麼其可能性會是什麼？ ->->-> `由於只有經過resolve執行就會以非同步形式來呼叫thenable的then方法，而獲取該promise object若是在call stack還有任務的情況下取得，那麼勢必為pending但僅僅限定於thenable或者正在處於pending狀態的promise object`
<!--SR:!2023-10-28,113,210-->

#🧠 Promise API 的 resolve(value)中的value 為thenable內容的話，會如何執行thenable？ ->->-> `只有經過resolve執行就會以非同步形式來呼叫thenable的then方法`
<!--SR:!2024-02-29,220,250-->



#🧠  Promise API 的 resolve 語法有哪些？ ->->-> `promise.resolve(value)、new Promise((resolve, _) => { /* ... */ resolve(value) })`
<!--SR:!2024-04-27,310,270-->

#🧠 Promise API 的 resolve(value) 語法會回傳較為具體的promise object，請問根據value的不同，其promise object可以會是哪些？ ->->-> `	- value 為 非thenable的內容或者不為promise object的話，promise.resolve就會回傳fulfilled狀態的promise object，其結果值會是value - value 為thenable的內容，promise.resolve就會回傳pending狀態的promise object。 - value 為promise object的內容，promise.resolve就會直接回傳該promise object`
<!--SR:!2023-09-21,2,247-->


#🧠 Promise API 的 resolve(value)中的value會是哪些 ->->-> `value 為 非thenable的內容或者不為promise object、thenable的內容、promise object的內容`
<!--SR:!2024-02-28,219,250-->

#🧠 Promise API 的 resolve(value)中的value若是非thenable或者不為promise object，會回傳什麼？ ->->-> `promise.resolve就會回傳fulfilled狀態的promise object，其結果值會是value`
<!--SR:!2024-02-29,220,250-->

#🧠 Promise API 的 resolve(value)中的value若是thenable，會回傳什麼？  ->->-> `promise.resolve就會回傳pending狀態的promise object`
<!--SR:!2024-01-18,199,250-->

#🧠 Promise API 的 resolve(value)中的value若是promise object，會回傳什麼？->->-> `promise.resolve就會直接回傳該promise object`
<!--SR:!2023-10-20,147,250-->


#🧠 `new Promise((resolve, _) => { /* ... */ resolve(value) }` 中的resolve為何要用resolve來取名，而非fulfilled？  ->->-> `由於其resolve功能本身就是將指定事物轉變成更為具體的事物，其事物可以fulfilled狀態或rejected或pending狀態的promise object，若是fulfilled的話，會無法說明其真正的用途`
<!--SR:!2024-01-20,167,230-->









---
Status: #🌱 
Tags:
[[JavaScript]] [[Promise]]
Links:
References:
[[@PromiseResolveJavaScript2023]]