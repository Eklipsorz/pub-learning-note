## 描述


[[@HowUsePromises]]
> **Promises** are the foundation of asynchronous programming in modern JavaScript. A promise is an object returned by an asynchronous function, which represents the current state of the operation.



[[@AsyncFunctionJavaScriptMDN]]
> The AsyncFunction object provides methods for async functions. In JavaScript, every async function is actually an AsyncFunction object.



[[@AsyncFunctionJavaScript]]
> async function 宣告被定義為一個回傳 AsyncFunction 物件的非同步函式 

```
async function name([param[, param[, ... param]]]) {
   statements
}
```

> 當 async 函式被呼叫時，它會回傳一個 Promise。如果該 async 函式回傳了一個值，Promise 的狀態將為一個帶有該回傳值的 resolved。如果 async 函式拋出例外或某個值，Promise 的狀態將為一個帶有被拋出值的 rejected。

> async 函式內部可以使用 await 表達式，它會暫停此 async 函式的執行，並且等待傳遞至表達式的 Promise 的解析，解析完之後會回傳解析值，並繼續此 async 函式的執行。


重點：
- promise 物件 本身代表著夾雜非同步任務內容、非同步任務執行狀態的物件，其物件主要由async function所回傳的或者使用Promise建構式，任務內容也是以async function或者建構式內的內容為主。
	- async function vs. promise object：前者是函式本身主要是回傳promise物件的函式並定義非同步任務是什麼；後者則是實際以物件形式來執行對應非同步任務並回報執行狀態。
- 若function 前綴標記成async的話，就會使function構成async function，具有以下功能：
	- 以function內容來定義promise的任務內容並回傳promise物件
	- 允許開發者在函式使用await語法糖

## 複習

#🧠 promise 在JavaScript上是什麼？ ->->-> `promise 物件 本身代表著夾雜非同步任務內容、非同步任務執行狀態的物件`
<!--SR:!2023-01-14,10,250-->

#🧠 promise 在JavaScript上本身是代表著夾雜非同步任務內容、非同步任務執行狀態的物件，那麼物件是誰產生？任務內容又是誰決定 ->->-> `其物件主要由async function所回傳的或者使用Promise建構式，任務內容也是以async function或者建構式內的內容為主。`
<!--SR:!2023-01-13,9,250-->

#🧠 javascript：async function vs. promise object 差異為何？ ->->-> `前者是函式本身主要是回傳promise物件的函式並定義非同步任務是什麼；後者則是實際以物件形式來執行對應非同步任務並回報執行狀態。`
<!--SR:!2023-01-13,9,250-->

#🧠 javascript： 如何將function設定為asynchronous  function？ ->->-> `若function 前綴標記成async的話，就會使function構成async function`
<!--SR:!2023-01-12,8,250-->



#🧠 javascript： 當將function設定為asynchronous  function時，該函式會有什麼功能->->-> `	- 以function內容來定義promise的任務內容並回傳promise物件 - 允許開發者在函式使用await語法糖`
<!--SR:!2023-01-05,1,210-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[await promise 會將後頭的多個任意語句全以promise.then來包裹住]]
[[當在async 函式內碰到指定await promise指派給特定識別字時，await會以分配記憶體來定義存放resolve的結果值，並賦予其識別字1，再以promise.then來設定resolve的結果值指派給識別字1所對應的內容]]
References:
[[@HowUsePromises]]
[[@AsyncFunctionJavaScript]]
[[@AsyncFunctionJavaScriptMDN]]