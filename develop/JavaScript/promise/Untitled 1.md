## 描述






### promise 所給予的inversion施加在inversion of control

promise 提供uninversion of control 概念來解決 inversion of control問題：
- 原本在Promise之前，開發者所定義的程式碼會由開發者來決定何時執行，但在非同步任務和callback處理時，會將callback轉由
- 概念為將inversion of control的概念在進行inverse，讓呼叫端主導callback的執行控制
- 原本實作前：呼叫端委派callback給指定非同步任務來執行，並且不等待非同步任務完成
- 原作實作後：呼叫端等待非同步任務完成，並由自己來執行callback



### promise 在程式開發上概念為

1. 預期特定任務回傳東西至特定程式模組(呼叫方)
2. 藉由呼叫方根據回傳結果來自行處理，從而不把程式的continuation交給另一方執行


#### inversion of control


- Inversion of Control (控制反轉) 
	- Inversion：特定事物在特定層面下的相反情況 
	- Control：誰決定誰的過程、方法，在一般開發上，常會將決定當成執行/使用，也就是誰執行/使用誰的過程、方法 
	- 總結起來會是指 誰決定誰的反轉 / 誰執行誰的反轉 ，比如程式區塊A執行程式區塊B，反轉後會是程式區塊B 執行 程式區塊 A、類別A繼承(使用)類別B，反轉後會是類別B繼承(使用)類別A。


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