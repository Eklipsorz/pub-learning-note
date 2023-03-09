## 描述


### promise 所給予的inversion施加在inversion of control


原本在Promise時代之前，呼叫端所定義的程式碼會由呼叫端來決定何時執行，但在將callback給予特定任務來處理時，會將callback轉由任務執行，這等同於變相地，由程式碼/第三方程式碼來決定呼叫端所定義的程式碼何時執行。

promise 面對inversion of control 問題之概念 或者uninversion：
- promise概念為將inversion of control的概念再次進行inverse，讓呼叫端主導callback的執行控制
- 原本實作前：
	- 呼叫端委派callback給指定任務來執行，不等任務完成
	- 使callback的執行權由任務來決定
- 原作實作後：
	- 呼叫端等待任務完成，並由呼叫端來執行callback
	- 使callback的執行權由呼叫端來決定



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
- promise 是指特定事物A聲稱特定事物A一定會去做特定事情的行為


## 複習

#🧠 JavaScript： 請描述在Promise 時代前所發生的callback問題 - inversion of control->->-> `原本在Promise時代之前，呼叫端所定義的程式碼會由呼叫端來決定何時執行，但在將callback給予特定任務來處理時，會將callback轉由任務執行，這等同於變相地，由程式碼/第三方程式碼來決定呼叫端所定義的程式碼何時執行。`
<!--SR:!2023-03-12,3,250-->

#🧠 JavaScript： Promise 面對inversion of control 問題之概念 或者uninversion會是什麼？->->-> `Promise概念為將inversion of control的概念再次進行inverse，讓呼叫端主導callback的執行控制`
<!--SR:!2023-03-12,3,250-->

#🧠  JavaScript： Promise 面對inversion of control 問題之概念 或者uninversion會是inversion of control的概念再次進行inverse，讓呼叫端主導callback的執行控制，那麼實作前和實作後會是什麼模式？請以呼叫端、callback、指定任務來說明->->-> `- 原本實作前： - 呼叫端委派callback給指定任務來執行，不等任務完成 - 使callback的執行權由任務來決定。原作實作後： - 呼叫端等待任務完成，並由呼叫端來執行callback  - 使callback的執行權由呼叫端來決定`
<!--SR:!2023-03-12,3,250-->


#🧠 promise 命名緣由會是什麼？？ ->->-> `promise 是指特定事物A聲稱特定事物A一定會去做特定事情的行為`
<!--SR:!2023-03-12,3,250-->

#🧠 JavaScript： Promise 面對inversion of control 問題之概念 或者uninversion會是inversion of control的概念再次進行inverse。上述若以程式來開發的話，其實現概念為何？->->-> `1. 預期特定任務回傳東西至特定程式模組(呼叫方) 2. 藉由呼叫方根據回傳結果來自行處理，從而不把程式的continuation交給另一方執行`
<!--SR:!2023-03-12,3,250-->

#🧠 inversion of control 中的 inversion 和 control 各為什麼意思？ ->->-> `	- Inversion：特定事物在特定層面下的相反情況  - Control：誰決定誰的過程、方法，在一般開發上，常會將決定當成執行/使用，也就是誰執行/使用誰的過程、方法 `
<!--SR:!2023-03-12,3,250-->

#🧠 inversion of control 在電腦科學會是指什麼？->->-> `總結起來會是指 誰決定誰的反轉 / 誰執行誰的反轉 ，比如程式區塊A執行程式區塊B，反轉後會是程式區塊B 執行 程式區塊 A、類別A繼承(使用)類別B，反轉後會是類別B繼承(使用)類別A。`
<!--SR:!2023-03-12,3,250-->

#🧠 inversion of control 在電腦科學會是指會是指 誰決定誰的反轉 / 誰執行誰的反轉，那麼會涉及哪些程式語言的範疇->->-> `OOP的繼承、模組間的依賴或者調用`
<!--SR:!2023-03-12,3,250-->








---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: