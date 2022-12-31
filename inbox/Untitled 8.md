## 描述


> async function 宣告被定義為一個回傳 AsyncFunction 物件的非同步函式 




[[@AsyncFunctionJavaScriptMDN]]
> The AsyncFunction object provides methods for async functions. In JavaScript, every async function is actually an AsyncFunction object.


```
async function name([param[, param[, ... param]]]) {
   statements
}
```

> 當 async 函式被呼叫時，它會回傳一個 Promise。如果該 async 函式回傳了一個值，Promise 的狀態將為一個帶有該回傳值的 resolved。如果 async 函式拋出例外或某個值，Promise 的狀態將為一個帶有被拋出值的 rejected。

> async 函式內部可以使用 await 表達式，它會暫停此 async 函式的執行，並且等待傳遞至表達式的 Promise 的解析，解析完之後會回傳解析值，並繼續此 async 函式的執行。





## 複習


---
Status: #🌱 
Tags:
Links:
References: