## 描述




promise 
1. 將現在執行解析到的內容和之後解析到的內容 正規化成 **之後** 這個時間點的內容
2. 目的為屏除何時執行、執行什麼，只專注之後會做


### promise 的universion of control

promise 提供uninversion of control 概念來解決 inversion of control問題：
- 概念為將inversion of control的概念在進行inverse，讓呼叫端主導callback的執行控制
- 原本實作前：呼叫端委派callback給指定非同步任務來執行，並且不等待非同步任務完成
- 原作實作後：呼叫端等待非同步任務完成，並由自己來執行callback


promise 在JS中會是指
1. 預期回傳東西至特定程式模組(呼叫方)
2. 藉由呼叫


在JS 中， 預期會是指回傳內容來給調用者



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