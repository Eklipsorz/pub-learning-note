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
- promise 本身以物件形式來包裝特定任務的執行過程，物件會包含任務內容、其對應執行狀態、其目前執行後的結果：
	- 特定任務可以是以同步執行形式來執行的任務 或者 以非同步執行形式來執行的任務
	- 狀態會由以下狀態所構成
		- pending：promise object 原有初始狀態，表示該object包裝的任務正等待執行
		- fulfilled： promise object 包裝的任務已成功完成執行 
		- rejected：promise object 包裝的任務執行是失敗的
- promise 語法形式會是：
	- resolve：
	- reject：
```
new Promise((resolve, reject) => {
	//.....
})
```
	
 - 回傳內容為promise object，具有兩種屬性分別為 state 和 result：

		- result：
	- fn 為夾雜resolve和reject函式物件的函式，其中resolve用以告知目前promise
```
new Promise(fn)

function fn(resolve, reject) {
	// ...
}
```

### then 方法

用途：
- 定義目前promise為fulfilled狀態時 或者 目前 promise 為rejected狀態時 所會做的事情



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


---
Status: #🌱 
Tags:
[[JavaScript]] [[Promise]]
Links:
[[由於promise本身只是官方規範，實作上會有許多不同版本，這使得很難判別誰到底是滿足官方規範的promise實作，並且從而透過它來開發。解法可以是thenable duck typing，但具有誤判的疑慮存在]]
References:
[[@javascript.infoPromise]]
[[@PromiseJavaScriptMDN2023]]
