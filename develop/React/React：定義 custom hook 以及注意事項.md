

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
- setInterval 排定一個重複執行的計時任務，等到指定毫秒才執行一次callback，接著再重新等待指定毫秒就會執行一次callback，直到手動中斷
- 任務內容會以func為主
- 任務數會一直產生，不會停止，除非手動停止
- setInterval 語法：
	- delay：設定幾毫秒(ms)才執行callback
	- callback：定義非同步任務的內容
```
setInterval(callback, delay)
```
#### setTimeout vs. setInterval 之間差別

[[@javascript.infoSchedulingSetTimeoutSetInterval]]

> We may decide to execute a function not right now, but at a certain time later. That’s called “scheduling a call”.

> There are two methods for it:
>-   `setTimeout` allows us to run a function once after the interval of time.
> -   `setInterval` allows us to run a function repeatedly, starting after the interval of time, then repeating continuously at that interval.

> These methods are not a part of JavaScript specification. But most environments have the internal scheduler and provide these methods. In particular, they are supported in all browsers and Node.js.

重點：
- setTimeout、setInterval 皆為指定特定時間點來執行特定處理的程式碼，具體會是以時間差來指定
- setTimeout：排定一個一次性計時任務，等到指定毫秒才執行一次callback
	- delay：設定幾毫秒(ms)才執行callback
	- callback：定義非同步任務的內容
```
setTimeout(callback, delay)
```
- setInterval：排定一個重複執行的計時任務，等到指定毫秒才執行一次callback，接著再重新等待指定毫秒就會執行一次callback，直到手動中斷
	- delay：設定幾毫秒(ms)才執行callback
	- callback：定義非同步任務的內容
```
setInterval(callback, delay)
```
- Node.js 和 瀏覽器都支援setTimeout 和 setInterval


### Interval 命名緣由

> a period between two events or times


重點：
- Interval：特定事件1和特定事件2之間的時間差



## 複習

#🧠 Interval 命名緣由為何？ ->->-> ` Interval：特定事件1和特定事件2之間的時間差`
<!--SR:!2024-09-22,426,250-->

#🧠 JS：setInterval 是什麼 ->->-> `排定一個重複執行的計時任務，等到指定毫秒才執行一次callback，接著再重新等待指定毫秒就會執行一次callback，直到手動中斷`
<!--SR:!2024-10-15,442,250-->

#🧠 JS：setInterval 語法為 ->->-> `setInterval(callback, delay)`
<!--SR:!2023-08-22,192,250-->

#🧠 JS：setInterval 語法為setInterval(callback, delay)，其中的callback和delay會是？->->-> `	- delay：設定幾毫秒(ms)才執行callback - callback：定義非同步任務的內容`
<!--SR:!2023-08-15,185,250-->

#🧠 JS：setInterval 和 setTimeout 之間差別？->->-> `setTimeout：排定一個一次性計時任務，等到指定毫秒才執行一次callback；setInterval：排定一個重複執行的計時任務，等到指定毫秒才執行一次`
<!--SR:!2025-01-30,508,250-->

#🧠 JS：setInterval 和 setTimeout 能在哪個執行環境下執行 ->->-> `瀏覽器和node.js`
<!--SR:!2023-08-04,169,230-->

#🧠 React：定義custom hook的條件為什麼？ ->->-> `1. 必須是function 2. function 名稱必須要是use 開頭`
<!--SR:!2023-08-19,189,250-->

#🧠 React：定義custom hook的條件為1. 必須是function 2. function 名稱必須要是use 開頭，若第二個不滿足的話，會是如何？->->-> `會被看待成一般函式`
<!--SR:!2024-12-09,480,250-->

#🧠 React：當function 名稱是use 開頭，React會如何看待和處理 ->->-> `React會直接視為hook，並且以hook function來檢查`
<!--SR:!2023-12-02,97,230-->


#🧠 React：開發custom hook會是如何開發？(比如放哪？以何種形式) ->->-> `每一個custom hook會以一個檔案來儲存，其檔案會儲存在/src/hooks`
<!--SR:!2023-08-20,189,250-->

#🧠 React：custom hook 若以檔案來儲存，會和其他元件同在同一個檔案進行開發嗎？->->-> `並不會`
<!--SR:!2024-03-22,248,230-->


#🧠 React：custom hook 若以檔案來儲存，且檔案內容只有hook，那麼檔名會是如何？通常來說 ->->-> `use-xxxx.js，xxxx 為功能名稱`
<!--SR:!2023-09-07,51,210-->




---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactBuildingYourOwn]]
[[@mdnSetIntervalWebAPIs]]
[[@javascript.infoSchedulingSetTimeoutSetInterval]]




