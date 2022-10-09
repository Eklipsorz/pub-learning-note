## 描述

### Bounce
>  When an object such as a ball bounces or when you bounce it, it moves upwards from a surface or away from it immediately after hitting it. 


> If something bounces or if something bounces it, it [swings](https://www.collinsdictionary.com/dictionary/english/swing "Definition of swings") or moves up and down.

[[@pomingleeDrLeeBlog2013]]
> 何謂 Bounce (彈跳)：   所謂的 Bounce 是指我們在按下電源開關時，電壓不會從 0 伏直接升到 VDD 伏。而是在 0 及 VDD 間震盪好幾次，最後才在 VDD 端穩定下來。

重點：
- bounce 是指特定事物只要經過特定反應，其位置會就以特定方向來回重複彈跳
- 在電腦科學裡，會是形容函式和調用者之間的回應速率就如同球經過打擊後的剛開始來回重複彈跳的速率：調用者呼叫函式，函式馬上回應調用者，接著調用者馬上呼叫函式，函式馬上回應調用者這樣子，該現象持續重複一段時間
- 請求方和處理方的回應速率是一個請求來臨，處理方就馬上處理當前請求的話，那麼在面對大量連續請求下，且目標是要取得最後一個請求作為處理，處理方在取得最後請求之前，會因為回應速率而產生以下現象：請求方發送一個請求，處理方接受到請求就處理；請求方又馬上發送請求，處理方接收到請求就馬上處理，後面以此類推。 該現象是bouncing

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
- debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。
- 背景：在連續發送事件觸發的場景下，處理方和請求方之間的回應速率會是請求方一發送請求，處理者就馬上處理請求，然而實際上卻是最後的事件觸發才是真正需要的，這導致拿到最後的事件觸發資訊之前，是有大量不必要的浪費都在前面的事件觸發處理上

- 具體策略會是以
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
<!--SR:!2022-10-28,28,250-->


#🧠 請以請求方和處理方的回應速率來說明bouncing現象 ->->-> ` 請求方和處理方的回應速率是一個請求來臨，處理方就馬上處理當前請求的話，那麼在面對大量連續請求下，且目標是要取得最後一個請求作為處理，處理方在取得最後請求之前，會因為回應速率而產生以下現象：請求方發送一個請求，處理方接受到請求就處理；請求方又馬上發送請求，處理方接收到請求就馬上處理，後面以此類推。 該現象是bouncing`
<!--SR:!2022-10-22,23,250-->

#🧠 bounce 在電腦科學裡的命名緣由是什麼？ ->->-> `會是形容函式和調用者之間的回應速率就如同球經過打擊後的剛開始來回重複彈跳的速率：調用者呼叫函式，函式馬上回應調用者，接著調用者馬上呼叫函式，函式馬上回應調用者這樣子，該現象持續重複一段時間`
<!--SR:!2022-10-27,28,250-->

#🧠 debouncing 的問題背景是什麼？ ->->-> `在連續發送事件觸發的場景下，處理方和請求方之間的回應速率會是請求方一發送請求，處理者就馬上處理請求，然而實際上卻是最後的事件觸發才是真正需要的，這導致拿到最後的事件觸發資訊之前，是有大量不必要的浪費都在前面的事件觸發處理上`
<!--SR:!2022-10-12,14,230-->


#🧠 debouncing 在電腦科學是什麼手段？ ->->-> `在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。`
<!--SR:!2022-10-28,28,250-->


#🧠 debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度，具體策略會是什麼？ ->->->  `每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步計時任務(timer task) - 生成一個非同步計時任務 (timer task)。每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步任務 - 生成一個非同步任務。使處理方等待一段時間在接收請求處理。 收集指定數量的請求數後再來處理`
<!--SR:!2022-10-28,28,250-->

#🧠 debouncing 在電腦開發實踐的手段：面對著大量連續請求下只想獲取最後一個請求來處理，那麼以使處理方等待指定時間在接收請求處理的潛在缺點會是什麼？(考量一下指定時間是否會變動) ->->-> `1. 若指定時間不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求2. 若指定時間會隨著執行狀況而變動，多少會比固定時間更容易保證`
<!--SR:!2022-11-09,31,248-->


#🧠 debouncing 在電腦開發實踐的手段：面對著大量連續請求下只想獲取最後一個請求來處理，那麼以收集指定數量的請求數後再來處理作為debouncing實現的潛在缺點會是什麼？(考量一下指定數量是否會變動) ->->-> `1. 若指定數量不會隨著執行狀況而變動，那麼很難保證處理方最後處理到的請求就是實際上的最後請求 2. 若指定數量會隨著執行狀況而變動，多少會比固定的指定數量更容易保證`
<!--SR:!2022-10-12,13,248-->



---
Status: #🌱 
Tags:
Links:
References: