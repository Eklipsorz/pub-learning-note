## 描述




當在async 函式內設定以下指派內容的語法時，
```
let temp = await Promise...
```

await在此會將其解析成：
	- 分配記憶體來定義存放resolve的結果值，並賦予其識別字1
	- 以promise.then來設定resolve的結果值指派給識別字1所對應的記憶體內容
```
// 分配記憶體
let temp = '';
Promise(....)
.then((ans) => {
	// 將resolve情況下的結果指派給temp
	temp = ans;
})
```


### 案例1

執行情況：首先先呼叫testAwaitFunction，而函式會回傳Promise物件並接著以非同步任務來做async函式內的程式碼，執行第一行時會先分配記憶體給res這個識別字，接著再將res的內容指派和await後續程式碼以promise.then來包覆著他們來執行。

當執行完promise時，就會以resolve情況下的1020指派給res這識別字，接著就印出1020和它會是數字，接著並以1020來回傳。
```
async function testAwaitFunction() {
  let res = await new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1020);
    }, 1000);
  });
  console.log(res, typeof res);
  return res;
}

console.log(testAwaitFunction());
```

執行情況：首先先呼叫testAwaitFunction，而函式會回傳Promise物件並接著以非同步任務來做async函式內的程式碼，執行第一行時，由於沒await，res會直接獲取到promise物件，該物件會呈現pending，接著生成promise非同步任務，後頭的console和return全會以夾帶著pending狀態的promise為主。

最後隨著event loop而執行到promise內的非同步任務執行，這時才會回傳resolve情況下的1020。

```
async function testAwaitFunction() {
  let res = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1020);
    }, 1000);
  });
  console.log(res, typeof res);
  return res;
}

console.log(testAwaitFunction());
```


### 案例2


執行情況：
當testAwaitFunction執行起來時，會定義一個物件obj，其中的res屬性會接著await promise，await碰到指派語句，會因為其的轉換方式使得res獲取到resolve的10，接著印出obj時會是擁有10的物件，最後並回傳
```
async function testAwaitFunction() {
  const obj = {
    res: await new Promise((resolve, _) => {
      setTimeout(() => {
        resolve(10);
      }, 1000);
    }),
  };
  console.log(obj);
  return obj;
}
```

## 複習

#🧠 當在async 函式內設定以下指派內容的語法`let temp = await Promise...` 會解析成什麼？->->-> `	- 分配記憶體來定義存放resolve的結果值，並賦予其識別字1 - 以promise.then來設定resolve的結果值指派給識別字1所對應的記憶體內容`
<!--SR:!2022-12-23,3,250-->

#🧠 當在async 函式內設定以下指派內容的語法`let temp = await Promise...` 會解析成什麼？以程式碼來說明->->-> `// 分配記憶體 let temp = ''; Promise(....).then((ans) => { // 將resolve情況下的結果指派給temp temp = ans; })`
<!--SR:!2023-01-02,10,250-->


#🧠 Promise程式碼的執行情況是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671465407/blog/javascript/promise/await/await-with-assignment-statement-example2_ee2qxh.png) ->->-> `首先先呼叫testAwaitFunction，而函式會回傳Promise物件並接著以非同步任務來做async函式內的程式碼，執行第一行時，由於沒await，res會直接獲取到promise物件，該物件會呈現pending，接著生成promise非同步任務，後頭的console和return全會以夾帶著pending狀態的promise為主。 最後隨著event loop而執行到promise內的非同步任務執行，這時才會回傳resolve情況下的1020。`
<!--SR:!2022-12-31,8,250-->

#🧠 Promise程式碼的執行情況是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671465407/blog/javascript/promise/await/await-with-assignment-statement-example1_apykcx.png) ->->-> `執行情況：首先先呼叫testAwaitFunction，而函式會回傳Promise物件並接著以非同步任務來做async函式內的程式碼，執行第一行時會先分配記憶體給res這個識別字，接著再將res的內容指派和await後續程式碼以promise.then來包覆著他們來執行。當執行完promise時，就會以resolve情況下的1020指派給res這識別字，接著就印出1020和它會是數字，接著並以1020來回傳。`
<!--SR:!2022-12-23,3,250-->

#🧠 Promise程式碼的執行情況是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671465407/blog/javascript/promise/await/await-with-assignment-statement-example3_rqdy8j.png) ->->-> `當testAwaitFunction執行起來時，會定義一個物件obj，其中的res屬性會接著await promise，await碰到指派語句，會因為其的轉換方式使得res獲取到resolve的10，接著印出obj時會是擁有10的物件，最後並回傳`
<!--SR:!2023-01-01,10,250-->




---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: