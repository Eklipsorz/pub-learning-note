## 描述


### 問題背景

useEffect 在遇到頻繁發送事件觸發的場景下是取得最近最新回應作為最後結果來處理的話，取得最近較新回應作為最後結果之前，會因為N個事件觸發而產生N個要執行effect的渲染請求，但這N個渲染請求的處理成本對於結論而言，是不必要的浪費


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

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：useEffect & Dependencies 之間關係就在於每一次effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行對應的callback]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]
References:
[[@mdnClearTimeoutWebAPIs]]
[[@pomingleeDrLeeBlog2013]]
[[@geeksforgeeksDebouncingJavaScript2018]]