## 描述


[[@javascript.infoPromise]]

```
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```
> The function passed to `new Promise` is called the _executor_. When `new Promise` is created, the executor runs automatically. It contains the producing code which should eventually produce the result. In terms of the analogy above: the executor is the “singer”.

> Its arguments `resolve` and `reject` are callbacks provided by JavaScript itself. Our code is only inside the executor.

> When the executor obtains the result, be it soon or late, doesn’t matter, it should call one of these callbacks:
> -   `resolve(value)` — if the job is finished successfully, with result `value`.
> -   `reject(error)` — if an error has occurred, `error` is the error object.

> So to summarize: the executor runs automatically and attempts to perform a job. When it is finished with the attempt, it calls `resolve` if it was successful or `reject` if there was an error.

> The `promise` object returned by the `new Promise` constructor has these internal properties:
> -   `state` — initially `"pending"`, then changes to either `"fulfilled"` when `resolve` is called or `"rejected"` when `reject` is called.
> -   `result` — initially `undefined`, then changes to `value` when `resolve(value)` is called or `error` when `reject(error)` is called.

> So the executor eventually moves `promise` to one of these states:

[[@PromiseJavaScriptMDN2023]]
> A `Promise` is in one of these states:

> -   _pending_: initial state, neither fulfilled nor rejected.
> -   _fulfilled_: meaning that the operation was completed successfully.
> -   _rejected_: meaning that the operation failed.



重點：
- promise 本身以物件形式來包裝特定任務、執行情況、其執行後的結果：
	- promise object 主要有state、result這兩種屬性
	- 特定任務可以是以同步執行形式來執行的任務 或者 以非同步執行形式來執行的任務
	- 狀態主要定義任務執行時的狀況，會由以下狀態所構成
		- pending：promise object 原有初始狀態，表示該object包裝的任務正等待執行
		- fulfilled： promise object 包裝的任務已成功完成執行 
		- rejected：promise object 包裝的任務執行是失敗的
	- 結果值會是目前任務執行時的結果：根據promise object的狀態而決定
		- 若是pending狀態的，就沒結果值
		- 若是fulfilled狀態，其結果值就為被解析出來的值
		- 若是rejected狀態，其結果值就為被解析出來的值
- promise 的建構式 語法形式會是：
	- resolve：為callback，主要將引數轉變成promise object，其狀態會是pending/fulfilled/rejected
	[[Promise.resolve(value)會將特定事物轉變成更為具體的promise object，並且其物件狀態會是fulfilled、rejected、pending]]
	- reject：為callback，主要將引數轉變成rejected狀態的promise object
```
new Promise((resolve, reject) => {
	//.....
})
```

### promise object的任務執行方式(非then、非catch)

只要一當對應promise object被建立，其包裝的任務內容會以同步形式來執行，如建立非同步任務(但不會立刻執行其非同步任務)

但這僅僅限定於最一開始被建立的Promise object


#### 案例
執行順序會是：
	- 建立Promise object
	- 執行command1
	- 執行command2
	- 建立非同步任務(不執行其任務內容)
	- 執行command3
	- 執行command4
	- 非同步任務執行
```
new Promise((resolve, reject) => {

	// command1
	// command2
	// create a async task
	// command3
})

// command4
```

### then 方法
[[@PromisePrototypeThen]]
> Parameters
		onFulfilled Optional
			A Function asynchronously called if the Promise is fulfilled. This function has one parameter, the fulfillment value. If it is not a function, it is internally replaced with an identity function ((x) => x) which simply passes the fulfillment value forward.

>		onRejected Optional
			A Function asynchronously called if the Promise is rejected. This function has one parameter, the rejection reason. If it is not a function, it is internally replaced with a thrower function ((x) => { throw x; }) which throws the rejection reason it received.


```
p.then(onFulfilled[, onRejected]);

p.then(function(value) {
  // fulfillment
}, function(reason) {
  // rejection
});
```

> Returns a new Promise immediately. This new promise is always pending when returned, regardless of the current promise's status.

用途：
- then 方法為promise object所擁有的方法之一，最主要是替 promise object 所定義的任務內容 註冊對應的事件處理：
	- 註冊 **任務執行成功的事件發生時，做些什麼**
	- 註冊 **任務執行失敗的事件發生時，做些什麼**
- 語法為：
	- onFulfilled：為callback，當監聽到的Promise p呈現的狀態為fulfilled時就以非同步任務形式來執行
	- onRejected：為callback，當監聽到的Promise p呈現的狀態為rejected時就以非同步任務形式來執行
	- onFulfilled 和 onRejected 的callback引數分別為：前者為resolved value，後者為系統攔截到的錯誤訊息物件或者reject方法的引數
	- then方法回傳promise物件，其狀態通常會因為event loop的關係而會是pending狀態
```
p.then(onFulfilled[, onRejected]);

p.then(
  (value) => { /* fulfillment handler */ },
  (reason) => { /* rejection handler */ },
)
```

### catch 方法
[[@PromisePrototypeCatch]]
> The catch() method of a Promise object schedules a function to be called when the promise is rejected. 

```
p.catch(onRejected)

p.catch((reason) => {
  // rejection handler
})
```


> Parameters
		onRejected
			A Function called when the Promise is rejected. This function has one parameter: the rejection reason.

> Return value
		Returns a new Promise. This new promise is always pending when returned, regardless of the current promise's status. It's eventually rejected if onRejected throws an error or returns a Promise which is itself rejected; otherwise, it's eventually fulfilled.

重點：
- catch 會是Promise object的方法之一，主要是替Promise object內部定義的任務註冊執行失敗時的事件處理
- 語法為
	- onRejected：為callback，主要當監聽的Promise object p呈現的狀態是rejected就以非同步任務形式來執行
	- onRejected 的callback引數為系統攔截到的錯誤訊息物件或者reject方法的引數
	- 回傳內容會是一個Promise object，其狀態會由於event loop的關係而總是pending狀態。
```
p.catch(onRejected)
p.catch((reason) => {
  // rejection handler
})
```


### then 方法和catch 方法的執行方式

監聽主要的promise object所擁有的狀態來執行，當狀態滿足時，就會以非同步來執行then或者catch所包含的callback


#### 案例
執行順序會是：
	- 建立Promise object
	- 執行command1
	- 執行command2
	- 建立非同步任務(不執行其任務內容)
	- 執行command3
	- 建立一個非同步任務來處理then的callback
	- 執行command4
	- 非同步任務執行
	- 執行callback
```
new Promise((resolve, reject) => {

	// command1
	// command2
	// create a async task
	// command3
})
.then(callback)

// command4
```

### 用語解釋

#### 狀態
pending：
> about to happen or waiting to happen


fulfilled：
> completed or achieved


rejected：
> If you reject something such as a proposal, a request, or an offer, you do not accept it or you do not agree to it.


重點：
- pending：將要發生或者等待發生的
- fulfilled：已完成/已達成的
- rejected：描述特定事物無法接受/無法滿足的。

## 複習


#🧠 用語解釋：pending是什麼意思？ ->->-> `將要發生或者等待發生的`
<!--SR:!2023-10-08,26,210-->

#🧠 用語解釋：fulfilled是什麼意思？ ->->-> `已完成/已達成的`
<!--SR:!2024-03-14,234,250-->

#🧠 用語解釋：rejected是什麼意思？ ->->-> `描述特定事物無法接受/無法滿足的`
<!--SR:!2023-10-24,124,210-->

#🧠 Promise API上的promise是什麼？ ->->-> `promise 本身以物件形式來包裝特定任務、執行情況、其執行後的結果`
<!--SR:!2024-01-19,199,250-->

#🧠  Promise API上的promise object 主要包含什麼屬性？ ->->-> `promise object 主要有state、result這兩種屬性`
<!--SR:!2024-01-28,205,250-->

#🧠 Promise API上的promise object 主要包含state、result這兩種屬性，這兩個屬性分別是什麼？ ->->-> `狀態主要定義任務執行時的狀況、結果值會是目前任務執行時的結果`
<!--SR:!2024-03-12,232,250-->

#🧠 Promise API上的promise object 主要包含state、result這兩種屬性，狀態主要定義任務執行時的狀況，會由哪些狀態所構成 ->->-> `- pending：promise object 原有初始狀態，表示該object包裝的任務正等待執行 - fulfilled： promise object 包裝的任務已成功完成執行  - rejected：promise object 包裝的任務執行是失敗的`
<!--SR:!2024-03-16,219,230-->

#🧠 Promise API上的promise object 主要包含state、result這兩種屬性，結果值會是目前任務執行時的結果，根據不同狀態下的promise object來說的話，其包含的結果會是？  ->->-> `	- 若是pending狀態的，就沒結果值 - 若是fulfilled狀態，其結果值就為被解析出來的值 - 若是rejected狀態，其結果值就為被解析出來的值`
<!--SR:!2024-03-02,222,250-->

#🧠 promise 的建構式 語法形式會是什麼？ ->->-> ``
<!--SR:!2023-12-31,184,250-->

#🧠  promise 的建構式 語法形式會是一個callback，其引數為兩個callback，分別為什麼？ ->->-> `resolve：為callback，主要將引數轉變成promise object，其狀態會是pending/fulfilled/rejected、reject：為callback，主要將引數轉變成rejected狀態的promise object`
<!--SR:!2024-03-23,243,250-->

#🧠 Promise API上的promise object擁有的then方法會是？ ->->-> `then 方法為promise object所擁有的方法之一，最主要是替 promise object 所定義的任務內容 註冊對應的事件處理`
<!--SR:!2024-02-19,210,250-->

#🧠 Promise API上的promise object擁有的then方法會是promise object所擁有的方法之一，最主要是替 promise object 所定義的任務內容 註冊對應的事件處理，其事件處理會是？->->-> `	- 註冊 **任務執行成功的事件發生時，做些什麼** - 註冊 **任務執行失敗的事件發生時，做些什麼**`
<!--SR:!2024-02-03,194,230-->

#🧠  Promise API上的promise object擁有的then方法會是promise object所擁有的方法之一，最主要是替 promise object 所定義的任務內容 註冊對應的事件處理，其事件處理若是以**任務執行成功的事件發生時，做些什麼** ，會是如何定義語法？ ->->-> `p.then((value) => { /* fulfillment handler */ })`
<!--SR:!2024-01-26,203,250-->


#🧠  Promise API上的promise object擁有的then方法會是promise object所擁有的方法之一，最主要是替 promise object 所定義的任務內容 註冊對應的事件處理，其事件處理若是以**註冊 **任務執行失敗的事件發生時，做些什麼** ，會是如何定義語法？ ->->-> `p.then((value) => { /* fulfillment handler */ }, (reason) => { .... })`
<!--SR:!2024-01-25,202,250-->

#🧠 Promise API上的promise object擁有的then語法會是什麼？ ->->-> `p.then(onFulfilled[, onRejected]);`
<!--SR:!2024-02-01,209,250-->

#🧠 Promise API上的promise object擁有的then語法會是`p.then(onFulfilled[, onRejected]);`，在這裡的onFulfilled和onRejected會是什麼？->->-> ` onFulfilled：為callback，當監聽到的Promise p呈現的狀態為fulfilled時就以非同步任務形式來執行、 onRejected：為callback，當監聽到的Promise p呈現的狀態為rejected時就以非同步任務形式來執行`
<!--SR:!2024-03-04,224,250-->

#🧠 Promise API上的promise object擁有的then語法會是`p.then(onFulfilled[, onRejected]);`，在這裡的onFulfilled和onRejected為callback，這兩個callback的引數分別會是什麼？ ->->-> ` onFulfilled 和 onRejected 的callback引數分別為：前者為resolved value，後者為系統攔截到的錯誤訊息物件或者reject方法的引數`
<!--SR:!2023-12-26,187,250-->

#🧠 Promise API上的promise object擁有的then語法回傳什麼？ ->->-> `then方法回傳promise物件`
<!--SR:!2024-01-24,184,230-->

#🧠 Promise API上的promise object擁有的then語法回傳Promise object，通常取得該object的狀態為何？ ->->-> `其狀態通常會因為event loop的關係而會是pending狀態`
<!--SR:!2024-01-27,204,250-->

#🧠 Promise API上的promise object擁有的catch 會是什麼？ ->->-> `catch 會是Promise object的方法之一，主要是替Promise object內部定義的任務註冊執行失敗時的事件處理`
<!--SR:!2024-01-18,195,250-->

#🧠 Promise API上的promise object擁有的catch語法 會是什麼？ ->->-> `p.catch(onRejected)`
<!--SR:!2023-11-19,135,230-->

#🧠 Promise API上的promise object擁有的catch語法 會是`p.catch(onRejected)`，那麼onRejected會是什麼？？ ->->-> `onRejected：為callback，主要當監聽的Promise object p呈現的狀態是rejected就以非同步任務形式來執行`
<!--SR:!2024-03-22,242,250-->

#🧠 Promise API上的promise object擁有的catch語法 會是`p.catch(onRejected)`，那麼onRejected會是callback，其callback的引數會是什麼？？ ->->-> `onRejected 的callback引數為系統攔截到的錯誤訊息物件或者reject方法的引數`
<!--SR:!2024-01-17,198,250-->

#🧠 Promise API上的promise object擁有的catch會回傳什麼？ ->->-> `回傳內容會是一個Promise object，其狀態會由於event loop的關係而總是pending狀態。`
<!--SR:!2024-03-20,240,250-->

#🧠 Promise API上的promise object擁有的catch會回傳promise object，當獲取其object時的狀態為何？ ->->-> `其狀態會由於event loop的關係而總是pending狀態。`
<!--SR:!2024-01-25,185,230-->


#🧠 這些指令、promise建立的執行順序是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677055220/blog/promise/execution/promise-object-task_cmxcu3.png) ->->-> `	- 建立Promise object - 執行command1 - 執行command2 - 建立非同步任務(不執行其任務內容) - 執行command3 - 執行command4 - 非同步任務執行`
<!--SR:!2023-11-25,98,229-->

#🧠 這些指令、promise建立的執行順序是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677055220/blog/promise/execution/promise-object-then-callback-task_a1vrrb.png) ->->-> `	- 建立Promise object - 執行command1 - 執行command2 - 建立非同步任務(不執行其任務內容) - 執行command3 - 建立一個非同步任務來處理then的callback - 執行command4 - 非同步任務執行 - 執行callback`
<!--SR:!2023-12-29,110,229-->

#🧠 只要一當對應promise object一被建立且該object為最一開始被建立的時候，其包裝的任務內容會是如何執行 ->->-> `只要一當對應promise object被建立，其包裝的任務內容會以同步形式來執行，如建立非同步任務(但不會立刻執行其非同步任務)`
<!--SR:!2023-11-19,82,229-->

#🧠 只要一當對應promise object被建立，其包裝的任務內容會以同步形式來執行，如建立非同步任務(但不會立刻執行其非同步任務)，promise object會限定於什麼條件才會這樣執行包裝的任務內容 ->->-> `這僅僅限定於最一開始被建立的Promise object`
<!--SR:!2024-03-18,238,249-->

#🧠 Promise API上的then 方法、catch方法的執行方式是如何？->->-> `監聽主要的promise object所擁有的狀態來執行，當狀態滿足時，就會以非同步來執行then或者catch所包含的callback`
<!--SR:!2024-04-02,246,249-->


---
Status: #🌱 
Tags:
[[JavaScript]] [[Promise]]
Links:
[[由於promise本身只是官方規範，實作上會有許多不同版本，這使得很難判別誰到底是滿足官方規範的promise實作，並且從而透過它來開發。解法可以是thenable duck typing，但具有誤判的疑慮存在]]
[[Promise.resolve(value)會將特定事物轉變成更為具體的promise object，並且其物件狀態會是fulfilled、rejected、pending]]
References:
[[@javascript.infoPromise]]
[[@PromiseJavaScriptMDN2023]]
[[@PromisePrototypeThen]]
[[@PromisePrototypeCatch]]
