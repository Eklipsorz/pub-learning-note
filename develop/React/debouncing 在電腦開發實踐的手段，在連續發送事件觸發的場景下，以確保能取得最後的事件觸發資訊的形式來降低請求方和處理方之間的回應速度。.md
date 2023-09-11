## 描述

### Bounce
>  When an object such as a ball bounces or when you bounce it, it moves upwards from a surface or away from it immediately after hitting it. 


> If something bounces or if something bounces it, it [swings](https://www.collinsdictionary.com/dictionary/english/swing "Definition of swings") or moves up and down.

[[@pomingleeDrLeeBlog2013]]
> 何謂 Bounce (彈跳)：   所謂的 Bounce 是指我們在按下電源開關時，電壓不會從 0 伏直接升到 VDD 伏。而是在 0 及 VDD 間震盪好幾次，最後才在 VDD 端穩定下來。


> What is debouncing?

> Debouncing is removing unwanted input noise from buttons, switches or other user input. 
> 
> Debouncing prevents extra activations or slow functions from triggering too often. 
> 
> Debouncing is used in hardware switches, programs and websites.

重點：
- bounce 是指特定事物只要經過特定反應，其位置會就以特定方向來回重複彈跳
- 在電腦科學裡的程式開發中，bounce會是指特定程式模組A在獲得正式事件/正式信號來處理前所發生 **程式模組所重複執行的事件處理或者信號處理**
-  **程式模組所重複執行的事件處理或者信號處理** 等同於以下動作的循環：
	- 程式模組接收信號來處理
	- 發送信號方發送信號至程式模組
	- 程式模組接收信號來處理
	- 發送信號方發送信號至程式模組
- 通常會將發送信號方最後所發送的事件或者信號正是正式事件/正式信號

### debouncing
[[@geeksforgeeksDebouncingJavaScript2018]]

> Debouncing in JavaScript is a practice used to improve browser performance. There might be some functionality in a web page which requires time-consuming computations. If such a method is invoked frequently, it might greatly affect the performance of the browser, as JavaScript is a single threaded language. Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page. In other words, it limits the rate at which a function gets invoked.


```
<html> 
<body>
<button id="debounce">
    Debounce
</button>
<script>
var button = document.getElementById("debounce");
const debounce = (func, delay) => {
    let debounceTimer
    return function() {
        const context = this
        const args = arguments
            clearTimeout(debounceTimer)
                debounceTimer
            = setTimeout(() => func.apply(context, args), delay)
    }
} 
button.addEventListener('click', debounce(function() {
        alert("Hello\nNo matter how many times you" +
            "click the debounce button, I get " +
            "executed once every 3 seconds!!")
                        }, 3000));
</script>
</body>
</html>
```


重點：
- de-bounce的de本身放在動詞前面，會是指去除/緩解動詞所要描述的現象，而debounce 會是指去除bounce或者緩解bounce的現象
- 在電腦科學裡的程式開發中的debounce主要有以下概要：
	- debounce 主要目的是效能優化，優化 **特定模組A遇到正式事件/正式信號並處理** 所需要花的成本
	- debounce 會是 去除/緩解特定模組A在獲得正式事件/正式信號來處理前所發生的重複執行的事件處理或者信號處理
	- 實現概念為：
		- 特定模組A停止執行所有額外信號或者事件的處理，直到接收到正式事件/正式信號才處理
		- 使特定模組A對於任一信號的接收處理速度變慢

- 案例：將最後一個所發送的事件視為正式事件/正式信號來處理，具體策略會是以
	- 每一次事件觸發的處理會是以
		- 清除上一個處理所產生的非同步計時任務(timer task)
		- 生成一個非同步計時任務 (timer task)
	- 每一次事件觸發的處理會是以
		- 清除上一個處理所產生的非同步任務
		- 生成一個非同步任務
	- 使處理方等待指定時間在接收請求處理
	- 收集指定數量的請求數後再來處理

#### 缺點：使處理方等待指定時間在接收請求處理
1. 若指定時間不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求
2. 若指定時間會隨著執行狀況而變動，多少會比固定時間更容易保證


#### 缺點：收集指定數量的請求數後再來處理

1. 若指定數量不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求
2. 若指定數量會隨著執行狀況而變動，多少會比固定的指定數量更容易保證




## 複習
#🧠 bounce 命名緣由是什麼？->->-> `特定事物只要經過特定反應，其位置會就以特定方向來回重複彈跳`
<!--SR:!2023-11-25,102,230-->


#🧠 在電腦科學中的程式開發中，bounce會是指什麼？ ->->-> ` bounce會是指特定程式模組A在獲得正式事件/正式信號來處理前所發生 **程式模組所重複執行的事件處理或者信號處理**`
<!--SR:!2023-06-14,56,228-->


#🧠 在電腦科學裡的程式開發中，bounce會是指特定程式模組A在獲得正式事件/正式信號來處理前所發生 **程式模組所重複執行的事件處理或者信號處理**，其中程式模組所重複執行的事件處理或者信號處理會是指什麼？舉例 ->->-> ` **程式模組所重複執行的事件處理或者信號處理** 等同於以下動作的循環：	- 程式模組接收信號來處理 - 發送信號方發送信號至程式模組 - 程式模組接收信號來處理 - 發送信號方發送信號至程式模組`
<!--SR:!2024-04-11,228,228-->

#🧠 在電腦科學裡的程式開發中，bounce會是指特定程式模組A在獲得正式事件/正式信號來處理前所發生 **程式模組所重複執行的事件處理或者信號處理**，其中的正式事件或者正式信號會是什麼？->->-> `通常會將發送信號方最後所發送的事件或者信號正是正式事件/正式信號`
<!--SR:!2023-06-24,99,248-->


#🧠 de-bounce的de本身放在動詞前面，de會是指什麼意思？ ->->-> `去除/緩解動詞所要描述的現象`
<!--SR:!2024-08-14,345,248-->


#🧠 de-bounce的de本身放在動詞前面，會是指去除/緩解動詞所要描述的現象，那麼debounce會是？->->-> `去除bounce或者緩解bounce的現象`
<!--SR:!2024-06-30,316,248-->


#🧠 在電腦科學裡的程式開發中的debounce，主要是為了什麼目標而出現以及實現？ ->->-> `debounce 主要目的是效能優化`
<!--SR:!2023-12-10,198,248-->

#🧠 在電腦科學裡的程式開發中的debounce，主要是為了什麼目標而出現以及實現？若是優化的話，會是指什麼？ ->->-> `，優化 **特定模組A遇到正式事件/正式信號並處理** 所需要花的成本`
<!--SR:!2024-03-12,253,248-->


#🧠 在電腦科學裡的程式開發中的debounce會是什麼？ ->->-> `去除/緩解特定模組A在獲得正式事件/正式信號來處理前所發生的重複執行的事件處理或者信號處理`
<!--SR:!2023-10-04,162,248-->

#🧠 debouncing 在前端開發上的問題背景是什麼？ ->->-> `在連續發送事件觸發的場景下，處理方和請求方之間的回應速率會是請求方一發送請求，處理者就馬上處理請求，然而實際上卻是最後的事件觸發才是真正需要的，這導致拿到最後的事件觸發資訊之前，是有大量不必要的浪費都在前面的事件觸發處理上`
<!--SR:!2023-07-01,104,248-->



#🧠 在電腦科學裡的程式開發中的debounce會是去除/緩解特定模組A在獲得正式事件/正式信號來處理前所發生的重複執行的事件處理或者信號處理，其中的去除或緩解的實現概念為何？ ->->-> `		- 特定模組A停止執行所有額外信號或者事件的處理，直到接收到正式事件/正式信號才處理- 使特定模組A對於任一信號的接收處理速度變慢 `
<!--SR:!2024-02-12,293,248-->

#🧠 在電腦科學裡的程式開發中的debounce會以什麼做為主要事件或者正式信號來處理？ ->->-> `將最後一個所發送的事件視為正式事件/正式信號來處理`
<!--SR:!2023-07-16,112,248-->



#🧠 debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度，具體策略會是什麼？ ->->->  `每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步計時任務(timer task) - 生成一個非同步計時任務 (timer task)。每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步任務 - 生成一個非同步任務。使處理方等待一段時間在接收請求處理。 收集指定數量的請求數後再來處理`
<!--SR:!2023-11-14,63,210-->

#🧠 debouncing 在電腦開發實踐的手段：面對著大量連續請求下只想獲取最後一個請求來處理，那麼以使處理方等待指定時間在接收請求處理的潛在缺點會是什麼？(考量一下指定時間是否會變動) ->->-> `1. 若指定時間不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求2. 若指定時間會隨著執行狀況而變動，多少會比固定時間更容易保證`
<!--SR:!2023-12-14,105,228-->


#🧠 debouncing 在電腦開發實踐的手段：面對著大量連續請求下只想獲取最後一個請求來處理，那麼以收集指定數量的請求數後再來處理作為debouncing實現的潛在缺點會是什麼？(考量一下指定數量是否會變動) ->->-> `1. 若指定數量不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求 2. 若指定數量會隨著執行狀況而變動，多少會比固定的指定數量更容易保證`
<!--SR:!2023-10-05,233,248-->



---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References: