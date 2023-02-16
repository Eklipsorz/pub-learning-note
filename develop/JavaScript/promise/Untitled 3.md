
## 描述



第一個參數就沒那麼容易決定了，它在Promise的相關文獻中常被標示為resolve(..)。這個用詞顯然與 **resolution (解析)** 有關。

但如果這個參數看似專門用來履行(fulfill) Promise，為何我們叫它resolve(..)，而不是應該更為正確的fulfill(..)呢？ 為了回答此問題，讓我們也看一下Promise API這兩個方法：
```
var fulfilledPr = Promise.resolve(42);
var rejectedPr = Promise.reject('Oops');
```


Pro


## 複習


---
Status: #🌱 
Tags:
[[JavaScript]] [[Promise]]
Links:
References: