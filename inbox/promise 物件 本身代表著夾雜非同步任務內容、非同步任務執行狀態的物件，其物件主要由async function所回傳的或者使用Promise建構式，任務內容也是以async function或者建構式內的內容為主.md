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
- 若function 前綴標記成async的話，就會使function構成async function物件，具有以下功能：
	- 以promise物件來包裝回傳內容
	- 允許開發者在函式使用await語法糖
- promise 物件 本身代表著夾雜非同步任務內容、非同步任務執行狀態的物件，其物件主要由async function所回傳的或者使用Promise建構式，任務內容是以建構式的定義內容為主。
	- async function vs. promise object：前者是以promise物件來包裝回傳內容；後者則是實際以物件形式來執行對應非同步任務並回報執行狀態。
- 若function 前綴標記成async的話，就會使function構成async function物件：
	- 若與一般的function比較起來，執行模式會是一樣，但除了回傳內容的包裝方式。
		- 若回傳內容是非promise的話，會以resolve狀態的promise物件來包裝回傳內容來回傳
		- 若回傳內容是promise A的話，就該promise A的狀態為主來回傳




### 範例

```
async function function1() {
  console.log('start');
  return 3
}
console.log(function1());
console.log('end');
```

```
start
Promise { 3 }
end
```


## 複習

#🧠 promise 在JavaScript上是什麼？ ->->-> `promise 物件 本身代表著夾雜非同步任務內容、非同步任務執行狀態的物件`
<!--SR:!2023-04-25,73,250-->

#🧠 promise 在JavaScript上本身是代表著夾雜非同步任務內容、非同步任務執行狀態的物件，那麼物件是誰產生？任務內容又是誰決定 ->->-> `其物件主要由async function所回傳的或者使用Promise建構式，任務內容是以建構式內的內容為主。`
<!--SR:!2023-03-18,45,246-->

#🧠 若function 前綴標記成async的話，就會使function構成async function物件，回傳內容的包裝方式會是如何？比如原本回傳非promise或者promise？promise狀態又是如何？ ->->-> `- 若回傳內容是非promise的話，會以resolve狀態的promise物件來包裝回傳內容來回傳 - 若回傳內容是promise A的話，就該promise A的狀態為主來回傳`
<!--SR:!2023-03-11,41,246-->

#🧠 若function 前綴標記成async的話，就會使function構成async function物件，該物件回傳的promise狀態又是如何？ ->->-> `- 若回傳內容是非promise的話，會以resolve狀態的promise物件來包裝回傳內容來回傳 - 若回傳內容是promise A的話，就該promise A的狀態為主來回傳`
<!--SR:!2023-05-07,73,246-->

#🧠 javascript：function前面添加async的話，會使function變成什麼物件？->->-> `async function物件`
<!--SR:!2023-03-02,35,246-->

#🧠 javascript：function前面添加async的話，會使function變成async function物件，那麼該物件和一般的function 物件的執行方式是如何？ ->->-> `都皆為同步執行`
<!--SR:!2023-03-12,41,246-->

#🧠 javascript：function前面添加async的話，會使function變成async function物件，那麼該物件和一般的function 物件 的相同點和不同點為何？？ ->->-> `相同點為都能同步執行，不同點為async function會將結果以promise物件來包裝以及允許使用await語法；後者並不會。`
<!--SR:!2023-03-21,44,226-->

#🧠 請問結果會是如何？又為何？`async function function1() { console.log('start'); return 3 } console.log(function1()); console.log('end');`->->-> `首先async function和一般function的執行方式一樣，會先印出start、最後將3包裝成resolve狀態的promise來回傳並印出對應promise物件，最後在印出end`
<!--SR:!2023-03-15,43,246-->


#🧠 請問function1()的回傳內容會是什麼？？`async function function1() { console.log('start'); return 3 } console.log(function1()); console.log('end');`->->-> `首先async function和一般function的執行方式一樣，會先印出start、最後將3包裝成resolve狀態的promise來回傳並印出對應promise物件`
<!--SR:!2023-03-16,44,246-->


#🧠 javascript：async function vs. promise object 差異為何？ ->->-> `前者是以promise物件來包裝回傳內容；後者則是實際以物件形式來執行對應非同步任務並回報執行狀態`
<!--SR:!2023-04-05,44,226-->


#🧠 javascript： 如何將function設定為asynchronous  function？ ->->-> `若function 前綴標記成async的話，就會使function構成async function`
<!--SR:!2023-04-04,58,250-->



#🧠 javascript： 當將function設定為asynchronous  function時，該函式會有什麼功能->->-> `		- 以promise物件來包裝回傳內容 - 允許開發者在函式使用await語法糖`
<!--SR:!2023-03-27,42,190-->

#🧠 javascript：async function是定義promise 為主的任務之內容嗎？為何？->->-> `並不是，最主要是由promise的建構式來定義內容`
<!--SR:!2023-03-16,17,226-->

#🧠 javascript：promise為主的任務內容誰負責定義？->->-> `會是由promise物件或者promise建構式來定義其內容`
<!--SR:!2023-02-28,34,246-->


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