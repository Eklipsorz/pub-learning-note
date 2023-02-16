
## 描述



> 第一個參數就沒那麼容易決定了，它在Promise的相關文獻中常被標示為resolve(..)。這個用詞顯然與 **resolution (解析)** 有關。

> 但如果這個參數看似專門用來履行(fulfill) Promise，為何我們叫它resolve(..)，而不是應該更為正確的fulfill(..)呢？ 為了回答此問題，讓我們也看一下Promise API這兩個方法：
```
var fulfilledPr = Promise.resolve(42);
var rejectedPr = Promise.reject('Oops');
```


> Promise.resolve(..) 創建一個會解析為所給的值的Promise。在這個例子中，42是一個普通的、非Promise、非thenable的值，所以就為42這個值創建了履行的承諾(fulfilled promise) fulfilledPr。Promise.reject('Oops')為'Oops' 這個理由創建了拒絕的承諾(rejected promise) rejectedPr。


> 現在讓我們說明為何 **resolve** 這個用語 (如Promise.resolve(..) 中所用的) 更加清楚也確實更為精確，如果是明確用在可能產生fulfillment 或者rejection 任一者的情境下的話：

```
var rejectedTh = {
	then: function(resolved, rejected) {
		rejected('Oops');
	}
}

var rejectedPr = Promise.resolve(rejectedTh);
```

> 如我們在本章前面討論過的，Promise.resolve(..) 會執行回傳所收到的真正Promise，或是解開收到的thenable。如果那個thenable的解開動作揭露出一個被拒絕的狀態，那麼從Promise.resolve(..)回傳的Promise實際上也會是相同的拒絕狀態。

> 所以Promise.resolve(..)是這個API方法良好且精確的名稱，因為他實際上可能會產生fulfillment或者rejection任一個狀態。

> Promise(..) 建構器的第一個callback參數會解開一個thenable(跟Promise.resolve(..)相同)或一個真正的Promise：

```
var rejectedPr = new Promise( function(resolve, reject) => {
	// 以一個被拒絕的Promise 來解析這個Promise
	resolve(Promise.reject('Oops'));
})

rejectedPr.then (
	function fulfilled() {
		// 永遠到不了這裡
	},
	function rejected(err) {
		console.log(error)
	}
);
```


### 

> If you resolve something into a clearer form, or if it resolves into a clearer form, its shape or the different parts it contains become clear.



## 複習


---
Status: #🌱 
Tags:
[[JavaScript]] [[Promise]]
Links:
References: