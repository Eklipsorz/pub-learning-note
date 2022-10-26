
## 描述
[[@AsynchronousWhatOrder]]
> the `await` keyword before the `doSomething()` function means that the rest of the code in the function after the `await` will be wrapped in a `then` call, giving control back to the caller of the function.




[[@mdnAwaitJavaScriptMDN]]
> The await operator is used to wait for a Promise and get its fulfillment value. It can only be used inside an async function or a JavaScript module.



重點：
- await 是一個operator，專門在async function裡等待promise為主的非同步任務完成
- async/await 本身是promise的語法糖，專門解決then chain 製造的巢狀問題，以試著讓開發難度/維護難度降低。
	- 實現手段為讓control flow更改成從上至下，而非從外至內來執行
- await 語法為
	- dosomething 為promise 為主的非同步任務
	- rest code 會是await dosomething 語句之後的任意多個語法/表達式，其中實際上會把這些語句全以dosomething這promise 的then 語法中當callback，如轉換後
```
await dosomething();
// rest code


// 轉換後
dosomething()
.then((...) => {
	// rest code
})
```


### 案例1

以下面為例，請問印出順序會是什麼？

常見的誤會是before -> setTimeout -> after -> end
但實際上會是before -> end -> setTimeout -> after
```
async function test() {
  console.log('before');
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('setTimeout');
      return resolve(1);
    }, 1000);
  });
  console.log('after');
}

test()
console.log('end');
```


### 案例2

```
async function test() {
  console.log('before');
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('setTimeout');
      return resolve(1);
    }, 1000);
  });
  console.log('after-1');
  console.log('after-2');
  console.log('after-3');
  console.log('after-4');
  console.log('after-5');
}

test()
console.log('end');
```

### 案例3

直接印出before -> end -> setTimeout -> 報錯

```
async function test() {
  console.log('before');
  await new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('setTimeout');
      return reject();
    }, 1000);
  });
  console.log('after-1');
  console.log('after-2');
  console.log('after-3');
  console.log('after-4');
  console.log('after-5');
}

test();
console.log('end');
```


#### control flow命名緣由
[[@ControlFlow2022]]
> In computer science, control flow (or flow of control) is the order in which individual statements, instructions or function calls of an imperative program are executed or evaluated.

control
>the act of controlling something or someone, or the power to do this

flow
>the movement of something in one direction



重點
- 在電腦科學裡，control flow 會是在imperative program中的特定語句/表達式/指令/函式呼叫的執行順序會是如何
- control 會是指擁有執行特定事物的權力、flow則是特定事物的流向，合併在一起就是執行控制權的交接流向 ：從一個特定指令A擁有執行權力並執行，接著切換成下一個指令擁有執行權力並執行
## 複習

#🧠 control 在電腦科學裡是指什麼？ ->->-> `擁有執行特定事物的權力`

#🧠 在電腦科學裡，control flow是什麼？ ->->-> `執行控制權的交接流向，從一個特定指令A擁有執行權力並執行，接著切換成下一個指令擁有執行權力並執行`

#🧠 在電腦科學裡，control flow是執行控制權的交接流向，白話點就是什麼？(指令、表達式的順序？)->->-> `在imperative program中的特定語句/表達式/指令/函式呼叫的執行順序會是如何`


#🧠 JS：async/await之前的promise會有什麼樣的問題？->->-> `then chain 製造的巢狀問題`


#🧠 JS：await 是什麼？ ->->-> `是一個operator，專門在async function裡等待promise為主的非同步任務完成`

#🧠 JS：async/await 對於 promise來說，是什麼 ->->-> `async/await 本身是promise的語法糖`

#🧠 JS：async/await 對於 promise來說是語法糖，為何需要這語法糖 ->->-> `專門解決then chain 製造的巢狀問題，以試著讓開發難度/維護難度降低`

#🧠 JS：async/await 對於 promise來說是語法糖，具體使開發難度降低，手段為何 ->->-> `實現手段為讓control flow更改成從上至下，而非從外至內來執行`
<!--SR:!2022-10-29,3,250-->

#🧠 JS：await 語法為何->->-> `await dosomething(); 

#🧠 JS：await 語法背後潛藏什麼樣語法？，以await dosomething();為例 ->->-> `await dosomething 語句之後的任意多個語法/表達式，其中實際上會把這些語句全以dosomething這promise 的then 語法中當callback。dosomething().then((...) => { // rest code })`

#🧠 JS：當在async function中出現這個 await dosomething(); // rest code，請問JS解析器會當成什麼來執行？->->-> `await dosomething 語句之後的任意多個語法/表達式，其中實際上會把這些語句全以dosomething這promise 的then 語法中當callback，`

#🧠 以下面為例，請問印出順序會是什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666700967/blog/javascript/promise/await/await-then-example1_uyqdc3.png) ->->-> `before -> end -> setTimeout -> after`

#🧠 以下面為例，請問印出順序會是before -> setTimeout -> after -> end嗎？為什麼 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666700967/blog/javascript/promise/await/await-then-example1_uyqdc3.png) ->->-> `並不是，實際正確順序為before -> end -> setTimeout -> after，這是因為await實際上會把後頭的程式碼全都會被該promise的then語法包裹住，以至於會先印出before之後，執行new promise來產生非同步任務，然後執行完畢之後，接著就印出end，最後promise中的時間到了就印setTimeout，最後有了resolve，then就跟著被觸發而執行after`



#🧠 以下面為例，請問印出順序會是什麼？  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666700967/blog/javascript/promise/await/await-then-example2_xuyml4.png) ->->-> `before -> end -> setTimeout -> after-1 -> after-2 -> .... -> after-5`


#🧠 以下面為例，請問印出順序會是什麼？   ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666701344/blog/javascript/promise/await/await-then-example3_l1luwz.png) ->->-> `before -> end -> setTimeout -> 報錯`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@ControlFlow2022]]
[[@AsynchronousWhatOrder]]
[[@mdnAwaitJavaScriptMDN]]