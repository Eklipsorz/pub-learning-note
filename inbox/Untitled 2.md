## 描述


每個keystroke都會觸發function component來渲染，而這等同於有每個keystroke會產生渲染請求，有N個keystrokes，就有N個渲染請求

  

有沒有一個機制能夠收集一定量的keystrokes 或者 你就只是等待一段足夠長的時間來處理請求.

  

比方說，使用者輸入字元時，就改在使用停止輸入字元的時候取得字元


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

> Debouncing is **a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page**. In other words, it limits the rate at which a function gets invoked


重點：
- debouncing 在電腦開發實踐的手段，降低降低函式和調用者之間的回應速率或者降低請求方和處理方之間的回應速度，確保較為耗時的任務別那麼快去接收到請求來處理
- 背景：函式和調用者之間的回應 或者 請求方和處理方之間的回應 本身是取最近的回應作為最後結果來處理
- 具體會是以
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

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@pomingleeDrLeeBlog2013]]
[[@geeksforgeeksDebouncingJavaScript2018]]