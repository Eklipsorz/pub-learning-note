## 描述




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


## 複習


---
Status: #🌱 
Tags:
Links:
References:
