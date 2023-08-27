## 描述


### 問題背景

[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]

> 在連續發送事件觸發的場景下，處理方和請求方之間的回應速率會是請求方一發送請求，處理者就馬上處理請求，然而實際上卻是最後的事件觸發才是真正需要的，這導致拿到最後的事件觸發資訊之前，是有大量不必要的浪費都在前面的事件觸發處理上


#### useEffect是否會遇到bounce問題？
會，具體是因為useEffect 所註冊的effect 面對接收到的請求都是一個請求被接收到就馬上被處理，所以會有有N個請求，就會有N個回應。


那麼若遇上連續發送事件觸發的場景下是要取得最後一個請求資訊的目標，勢必在取得最後一個請求資訊之前會有大量不必要的請求處理浪費著資源


### 解決目標
為了能在頻繁發送事件觸發的場景下是取得最近最新回應 並且 盡可能減少在取得之前的請求處理成本，會採用以下策略：
	- 每一次事件觸發的處理會是以
		- 清除上一個處理所產生的非同步計時任務(timer task)
		- 生成一個非同步計時任務 (timer task)
	- 每一次事件觸發的處理會是以
		- 清除上一個處理所產生的非同步任務
		- 生成一個非同步任務


[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]
#### 使用setTimeout + cleanup
在這裡是採取
	- 每一次事件觸發的處理會是以
		- 清除上一個處理所產生的非同步計時任務(timer task)
		- 生成一個非同步計時任務 (timer task)
實現方式為：
- 每一次effect觸發就清除上一個effect觸發處理生成的非同步計時任務(timer task)：以effect 的cleanup來實現，其identifier會是記錄上一個處理而生成的計時任務ID
```
return () => {
		clearTimeout(identifier);
}
```
- 為當前effect觸發處理而生成一個非同步計時任務：以setTimeout(callback,500)來生成非同步任務，並回傳其任務ID作為cleanup的依據
```
    const identifier = setTimeout(() => {
	    // do something
	    setState(....);
    }, 500);
```


最後會是：

```
 useEffect(() => {
    const identifier = setTimeout(() => {
	    // do something
	    setState(....);
    }, 500);

	return () => {
		clearTimeout(identifier);
	}
	
  }, dependencies);
```


如果我們想要去透過UI的互動來送http 請求，若同樣以最近結果作為最後結果來處理，那麼就能使用setTimeout和cleanup來處理，以確保最後請求只會是一個且會是以最新最近的結果來發送



### cleanup function

[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]



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

## 複習

#🧠 React：若要以非同步計時任務來實現debouncing的概念，具體要做什麼？ ->->-> `每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步計時任務(timer task) - 生成一個非同步計時任務 (timer task)。 每一次事件觸發的處理會是以： - 清除上一個處理所產生的非同步任務 - 生成一個非同步任務`
<!--SR:!2023-11-30,95,210-->
`

#🧠  React：如何在useEffect實現以下debouncing的概念：每一次事件觸發的處理會是以 - 清除上一個處理所產生的非同步計時任務(timer task) - 生成一個非同步計時任務 (timer task)->->-> `在useEffect 使用setTimemout 來夾雜side effect原本實現代碼，然後紀錄當前的timeout的任務ID，定義著useEffect的cleanup來依照timeoue任務ID來取消任務。`
<!--SR:!2023-09-11,206,230-->

#🧠 React：useEffect是否會遇到bounce問題？為什麼 ->->-> `會，具體是因為useEffect 所註冊的effect 面對接收到的請求都是一個請求被接收到就馬上被處理，所以會有N個請求，就會有N個回應。`
<!--SR:!2023-10-28,243,247-->


#🧠 React：如何在useEffect的debouncing 實現是在useEffect 使用setTimemout 來夾雜side effect原本實現代碼，然後紀錄當前的timeout的任務ID，定義著useEffect的cleanup來依照timeoue任務ID來取消任務，那麼實際如何執行？如何確保就是最後一個請求？->->-> `首次元件開始mounting就生成setTimeout任務，並定義cleanup任務是要清除掉當前timeout的任務，接著若下一個effect被觸發就先執行cleanup任務來清除上一個timeout非同步任務，然後重新生成timeout任務，接著定義cleanup來清除這次生成的timeout任務，後面依此類推，直到沒觸發，代表當前timeout任務正執行著最後一個請求。`
<!--SR:!2025-02-04,537,250-->

#🧠 React：在useEffect的debouncing 實現中，是如何實現每一次effect觸發就清除上一個effect觸發處理生成的非同步計時任務(timer task) ->->-> `以effect 的cleanup來實現，其identifier會是記錄上一個處理而生成的計時任務ID。定義effect的cleanup任務，內容為return () => { clearTimeout(identifier); }`
<!--SR:!2025-02-04,527,250-->

#🧠 React：在useEffect的debouncing 實現中， 是如何實現為當前effect觸發處理而生成一個非同步計時任務->->-> `以setTimeout(callback,500)來生成非同步任務，並回傳其任務ID作為cleanup的依據 const identifier = setTimeout(() => { // do something setState(....); }, 500);`
<!--SR:!2025-01-26,530,250-->

#🧠 React：以下是使用setTimeout + cleanup 來實現的debouncing代碼，請問其中的clearTimeout的identifier會是什麼？，若下一個side effect執行時執行cleanup又是指哪個identifier![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663348476/blog/react/effect/setTimeout_cleanup_debouncing_vgcmnr.png) ->->-> `會是設定當前產生出來timeout任務ID，並於下一個side effect執行前就執行cleanup的identifier會是指上一個effect產生出來的timeout任務ID`
<!--SR:!2023-08-10,196,247-->


#🧠 React：請用setTimeout + cleanup 程式碼來實現effect的debouncing概念 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663348476/blog/react/effect/setTimeout_cleanup_debouncing_vgcmnr.png)`
<!--SR:!2023-07-23,194,250-->

---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行side effect]]
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]
References:
[[@mdnClearTimeoutWebAPIs]]
[[@pomingleeDrLeeBlog2013]]
[[@geeksforgeeksDebouncingJavaScript2018]]