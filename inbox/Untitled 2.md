## 描述


### 問題背景

useEffect 在遇到頻繁發送事件觸發的場景下是取得最近最新回應作為最後結果來處理的話，取得最近較新回應作為最後結果之前，會因為N個事件觸發而產生N個要執行effect的渲染請求，但這N個渲染請求的處理成本對於結論而言，是不必要的浪費


### 解決目標
為了能在頻繁發送事件觸發的場景下是取得最近最新回應 並且 盡可能減少在取得之前的請求處理成本，會採用以下策略：
- debouncing：放緩effect的處理速度 + 利用放緩來清除不必要的任務
- 等待一定數量的請求量，並合併處理，比如說使用者輸入內容時就等待，輸入完就以最後結果為主

#### 使用setTimeout + cleanup
在這裡是採取
	-  放緩effect的處理速度 + 利用放緩來清除不必要的任務
實現方式為：
	- 在useEffect的callback中，每一個請求會產生一個500ms後才執行的setTimeout任務來做side effect


```
 useEffect(() => {
    setTimeout(() => {
	    // do something
	    setState(....);
    }, 500);
  }, dependencies);
```

結果：
- 藉由放緩effect的處理速度，
- 

潛在問題：
- 每接收一個請求
- 若索要的結果是N個事件觸發中的最後一個事件觸發，會



每個keystroke都會觸發function component來渲染，而這等同於有每個keystroke會產生渲染請求，有N個keystrokes，就有N個渲染請求

  

有沒有一個機制能夠收集一定量的keystrokes 或者 你就只是等待一段足夠長的時間來處理請求.

  

比方說，使用者輸入字元時，就改在使用停止輸入字元的時候取得字元


為了實現debounce而衍生出來的timer，若前面部分timer任務結果已經達成目標，那麼可以考慮清除後面多出來的timer，以節省後續的timer 成本

  

useEffect cleanup 技術能夠清除掉多出來負責執行side effect的任務，以確保效能不會受損

```
useEffect( () => {
   ....
   return callback
}), [...] )
```


實際會以useEffect 所回傳的callback來定義如何清除多出來的side effect 任務

callback 可以是匿名、箭頭、命名

  

當渲染週期到了且滿足dependency，React 會先透過useEffect 最一開始的callback執行，並取得對應callback，來當作清除用，順序會是

useEffect(callback)-> cleanup = callback(...) -> run cleanup

> before useEffect executes this function the next time / before every new side effect function execution and before the component is removed And it does not run before the first side effect function execution

  

除了第一次side effect 函式之前不會執行以外，在其他下一次side effect執行之前 就清除或者component被移除之前就清除









```
useEffect( () => {
   setTimeOut(callback2, xxx);
   return callback3
}), [...] )

```

  

由於cleanup 的特性和useEffect(callback1)特性，使得只有一個setTimeOut會被執行，剩餘的setTimeOut都會因為cleanup的特性-下一個side effect之前執行callback3來清除setTimeOut任務，而唯一的setTimeOut任務會是使用者最近輸入的內容


如果我們想要去透過UI的互動來送http 請求，若同樣以最近結果作為最後結果來處理，那麼就能使用setTimeout和cleanup來處理，以確保最後請求只會是一個且會是以最新最近的結果來發送

### useEffect cleanup function


### clearTimout 功用

[[@mdnClearTimeoutWebAPIs]]
>  The global clearTimeout() method cancels a timeout previously established by calling setTimeout().

> If the parameter provided does not identify a previously established action, this method does nothing. 

```
clearTimeout(timeoutID)
```


重點：
- clearTimeout 取消還未執行完成的setTimeout任務
- clearTimeout(timeoutID) 的 timeoutID ：
	- timeoutID 是 timeout任務ID
	- timeoutID 可以setTimeout那邊取得

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
[[React：useEffect & Dependencies 之間關係就在於每一次effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行對應的callback]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
References:
[[@mdnClearTimeoutWebAPIs]]
[[@pomingleeDrLeeBlog2013]]
[[@geeksforgeeksDebouncingJavaScript2018]]