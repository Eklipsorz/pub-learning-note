## 描述

### Bounce
>  When an object such as a ball bounces or when you bounce it, it moves upwards from a surface or away from it immediately after hitting it. 


> If something bounces or if something bounces it, it [swings](https://www.collinsdictionary.com/dictionary/english/swing "Definition of swings") or moves up and down.

[[@pomingleeDrLeeBlog2013]]
> 何謂 Bounce (彈跳)：   所謂的 Bounce 是指我們在按下電源開關時，電壓不會從 0 伏直接升到 VDD 伏。而是在 0 及 VDD 間震盪好幾次，最後才在 VDD 端穩定下來。

重點：
- bounce 是指特定事物只要經過特定反應，其位置會就以特定方向來回重複彈跳
- 在電腦科學裡，會是形容函式和調用者之間的回應速率就如同球經過打擊後的剛開始來回重複彈跳的速率：調用者呼叫函式，函式馬上回應調用者，接著調用者馬上呼叫函式，函式馬上回應調用者這樣子，該現象持續重複一段時間

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
- 背景：在連續發送事件觸發的場景下，處理方和請求方之間的回應速率會是請求方一發送請求，處理者就馬上處理請求，然而實際上卻是最後的事件觸發才是真正需要的，這導致拿到最後的事件觸發資訊之前，是有大量不必要的浪費

- 具體策略會是以
	- 強迫等待一段特定時間
	- 收集指定數量的請求數後再來處理


#### 案例 debouncing

```
  useEffect(() => {
    setFormIsValid(
      enteredEmail.includes('@') && enteredPassword.trim().length > 6,
    );
  }, [enteredEmail, enteredPassword]);
```


```
useEffect(() => {
	setTimeout(() => {
		setFormIsValid(
			enteredEmail.includes('@') && enteredPassword.trim().length > 6,
		);
	}, 500);
}, [enteredEmail, enteredPassword]);
```



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 #📓 
Tags:
Links:
References: