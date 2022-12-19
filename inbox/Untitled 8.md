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
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: