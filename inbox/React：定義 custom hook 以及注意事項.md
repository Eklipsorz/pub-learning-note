
## 描述


### 開發custom hook的注意事項

custom hook ：
- 通常會將hook function 以一個單一檔案來儲存，檔名通常會取use-xxxx.js，xxxx為功能名
- hook function 放置在/src/hooks




### 定義custom hook的條件


[[@reactBuildingYourOwn]]
> **A custom Hook is a JavaScript function whose name starts with ”`use`” and that may call other Hooks**

1. 必須是function
2. function 名稱必須要是use 開頭：當被設定時，react會開始檢查其他條件是否滿足成為hook的條件


若不滿足的話，會被當作一般函式看待。


### setInterval() 用法

[[@mdnSetIntervalWebAPIs]]
> The setInterval() method, offered on the Window and Worker interfaces, repeatedly calls a function or executes a code snippet, with a fixed time delay between each call. 

```
setInterval(func, delay)
```


重點：
- setInterval 產生一個非同步計時任務，該任務會按照delay給予的秒數來自動生成一個非同步任務
- 任務內容會以func為主
- 任務數會一直產生，不會停止，除非手動停止
#### setTimeout vs. setInterval 之間差別

[[@javascript.infoSchedulingSetTimeoutSetInterval]]

> We may decide to execute a function not right now, but at a certain time later. That’s called “scheduling a call”.

> There are two methods for it:
>-   `setTimeout` allows us to run a function once after the interval of time.
> -   `setInterval` allows us to run a function repeatedly, starting after the interval of time, then repeating continuously at that interval.

> These methods are not a part of JavaScript specification. But most environments have the internal scheduler and provide these methods. In particular, they are supported in all browsers and Node.js.

重點：
- setTimeout、setInterval 皆為指定特定時間點來執行特定處理的程式碼，具體會是以時間差來指定
- setTimeout：排定一個計時任務，等到指定毫秒才執行一次callback
	- delay：設定幾毫秒(ms)才執行callback
	- callback：定義非同步任務的內容
```
setTimeout(callback, delay)
```
- setInterval：排定一系列同內容的非同步任務來執行，每一個任務都必須等到指定毫秒才執行，執行完就會等待下一個同個指定毫秒來執行下一個同個任務內容的任務
	- delay：設定幾毫秒(ms)才執行callback
	- callback：定義非同步任務的內容
```
setInterval(callback, delay)
```
- Node.js 和 瀏覽器都支援setTimeout


### Interval 命名緣由

> a period between two events or times


重點：
- Interval：特定事件1和特定事件ㄉ之間的時間差



## 複習

#🧠 Interval 命名緣由為何？ ->->-> ``

#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactBuildingYourOwn]]
[[@mdnSetIntervalWebAPIs]]
[[@javascript.infoSchedulingSetTimeoutSetInterval]]




