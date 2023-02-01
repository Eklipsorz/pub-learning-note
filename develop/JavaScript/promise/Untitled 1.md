## 描述






### promise 的universion of control

promise 提供uninversion of control 概念來解決 inversion of control問題：
- 概念為將inversion of control的概念在進行inverse，讓呼叫端主導callback的執行控制
- 原本實作前：呼叫端委派callback給指定非同步任務來執行，並且不等待非同步任務完成
- 原作實作後：呼叫端等待非同步任務完成，並由自己來執行callback



### promise 在程式開發上概念為

1. 預期特定任務回傳東西至特定程式模組(呼叫方)
2. 藉由呼叫方根據回傳結果來自行處理，從而不把程式的continuation交給另一方執行





#### 具體實現
將promise object 定調為特定任務會回傳未來值的憑據，該object會夾雜定義特定任務如何執行和執行狀態，並讓呼叫方監聽憑據兌現才執行對應的callback


特定任務上本身會區分成同步和非同步的執行模式，若為前者的話，很容易
具體來說會將：
1. 將現在執行解析到的內容和之後解析到的內容 兩者的時間 正規化成 **之後** 這個時間點的內容
2. 目的為屏除何時執行、執行什麼，只專注未來會回傳特定結果。

##### 正規化時間的原因
若參與處理或者計算的內容會是現在取得到的內容和未來取得的內容，但最後肯定會在未來的時間點來決定其計算或者處理的結果，因此將內容區分成現在和未來是無意義，畢竟都會在未來才開始處理，所以會將現在取得到的內容和未來取得到的內容都視為未來取得到的內容


#### promise 命名緣由

> the act of saying that you will certainly do something

重點：
- promise 是指說特定事物一定會去做特定事情的行為


## 複習



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: