
## 描述

> the `await` keyword before the `doSomething()` function means that the rest of the code in the function after the `await` will be wrapped in a `then` call, giving control back to the caller of the function.


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


// before -> setTimeout -> after -> end
```


## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@AsynchronousWhatOrder]]