
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
  console.log('after');
}

test()
console.log('end');

```

## 複習

#🧠 JS：await 是什麼？ ->->-> `是一個operator，專門在async function裡等待promise為主的非同步任務完成`

#🧠 JS：async/await 對於 promise來說，是什麼 ->->-> `async/await 本身是promise的語法糖`

#🧠 JS：async/await 對於 promise來說是語法糖，為何需要這語法糖 ->->-> `專門解決then chain 製造的巢狀問題，以試著讓開發難度/維護難度降低`

#🧠 JS：async/await 對於 promise來說是語法糖，具體使開發難度降低，手段為何 ->->-> `實現手段為讓control flow更改成從上至下，而非從外至內來執行`

#🧠 Question :: ->->-> ``


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@AsynchronousWhatOrder]]
[[@mdnAwaitJavaScriptMDN]]