


### 若chain中出現錯誤或者rejected狀態的promise
[[@PromisePrototypeThen2022]]

> **備註：** 如果有一個或兩個引數被省略，或為非函式（non-functions），則 `then` 將處於遺失 handler(s) 的狀態，但不會產生錯誤。若發起 `then` 之 `Promise` 採取了一個狀態（實現（`fulfillment）`或拒絕（`rejection））`而 `then` 沒有處理它的函式，一個不具有額外 handlers 的新 `Promise` 物件將被建立，單純採取原 `Promise` 其最終狀態。

[[@PromisePrototypeThen]]
> onRejected Optional
		A Function asynchronously called if the Promise is rejected. This function has one parameter, the rejection reason. If it is not a function, it is internally replaced with a thrower function ((x) => { throw x; }) which throws the rejection reason it received.

自動解開rejected狀態的promise所夾雜的錯誤資訊

## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@PromisePrototypeThen2022]]
[[@PromisePrototypeThen]]