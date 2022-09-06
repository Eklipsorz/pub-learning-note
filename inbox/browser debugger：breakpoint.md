## 描述

### browser debugger：breakpoint


> but it also gives the browser extra information which the browser developer tools are able to pick up to allow us to actually debug our code in the raw form we wrote it in

react development 工具會在結果網頁中賦予瀏覽器一些資訊：
1. 用webpack轉換前的原始碼，以便除錯
	- 位置會在/Users/xxxx.... 目錄下的src目錄

#### step into next function call 

[[@ithomeDay13Sources]]
> ### Step into next function call

> 如果即將執行的 Function 正是問題所在，`Step into` 會停在該 Function 內的第一行。
> 假設目前暫停在 A 行的 `double`

```javascript
const number = 3;
const result = double(number); // A
console.log(result); // D

function double(n) {
  const result = n * 2; // B
  return result; // C
}
```

> 點擊圖示後會跳至 B 行，也就是 `double` 的第一行。


重點：
- step into next function call ：
	- 若目前斷點不是夾帶著其他函式呼叫的程式碼的話，按下 step into next function call 只會往下一行執行並停止
	```
	-> console.log('hi')
	```
	- 若目前斷點是夾帶著其他函式的程式碼的話，按下 step into next function 會往被呼叫函式那裡執行並於函式第一行停止
	```
	-> const result = double(number); // A
	function double(n) {
	  const result = n * 2; // B
	  return result; // C
	}
	```
#### Step over next function call

> ### Step over next function call
> 如果對即將執行的 Function 內部沒有興趣，`Step over` 會跳至該 Function 後方。
>
> 以下方程式碼為例，假設目前暫停在 A 行的 `double`：

```javascript
const number = 3;
const result = double(number); // A
console.log(result); // D

function double(n) {
  const result = n * 2; // B
  return result; // C
}
```

> 點擊圖示後會執行 `double` 內的所有程式碼並停在 D 行的 `console.log`。

重點：
- step over next function call ：
	- 若目前斷點不是夾帶著其他函式呼叫的程式碼的話，按下 step over next function call 只會往下一行執行並停止
	```
	-> console.log('hi')
	```
	- 若目前斷點是夾帶著其他函式的程式碼的話，按下 step over next function 會跳過被呼叫函式並執行下一行停止
	```
	-> const result = double(number); // A
	function double(n) {
	  const result = n * 2; // B
	  return result; // C
	}
	```


### breakpoint 命名緣由

[[@wikidataDuanDian2021]]
> 斷點（英語：Breakpoint）是程式中為了除錯而故意停止或者暫停的地方。

> 除錯設定斷點可以讓程式執行到該行程式時停住，藉此觀察程式到斷點位置時，其變數、暫存器、I/O等相關的變數內容，有助於深入了解程式運作的機制，發現、排除程式錯誤的根源。 

[[@wikidataBreakpoint2022]]
> In software development, a breakpoint is an intentional stopping or pausing place in a program, put in place for debugging purposes. It is also sometimes simply referred to as a pause. 

重點：
- breakpoint ：在程式中，設定特定程式碼位置為暫時停止/中斷的地方，當程式執行到那個位置就會停止，並透露那時的執行狀態
- breakpoint 用途：
	- 查看特定時機點時的狀態

### break 命名緣由
break：
> to interrupt or to stop something for a short period
	打斷；中斷，中止

重點：
- 暫時停止特定行為/中斷特定行為

## 複習

#🧠 break 命名緣由是什麼？ ->->-> `暫時停止特定行為/中斷特定行為`
<!--SR:!2022-09-09,3,250-->

#🧠 breakpoint 命名緣由是什麼？ ->->-> `在程式中，設定特定程式碼位置為暫時停止/中斷的地方，當程式執行到那個位置就會停止，並透露那時的執行狀態`

#🧠 breakpoint 主要用途是什麼？ ->->-> `查看特定時機點時的狀態`

#🧠 為什麼瀏覽器會知道react專案被webpack處理前的程式碼？ ->->-> `react development 工具會在結果網頁中賦予瀏覽器一些資訊`

#🧠 react development 工具會在結果網頁中賦予瀏覽器一些資訊，比如？ ->->-> `用webpack轉換前的原始碼，以便除錯`
<!--SR:!2022-09-09,3,250-->

#🧠 若目前斷點不是夾帶著其他函式呼叫的程式碼的話，按下 step into next function call 會往哪邊走？ ->->-> `下一行執行並停止`

#🧠 若目前斷點是夾帶著其他函式的程式碼的話，按下 step into next function call 會往哪邊走？->->-> `往被呼叫函式那裡執行並於函式第一行停止`
<!--SR:!2022-09-09,3,250-->

#🧠 若目前斷點不是夾帶著其他函式呼叫的程式碼的話，按下 step over next function call 會往哪邊走？ ->->-> `下一行執行並停止`
<!--SR:!2022-09-09,3,250-->

#🧠 若目前斷點是夾帶著其他函式的程式碼的話，按下 step over next function 會往哪邊走？ ->->-> `會跳過被呼叫函式並執行下一行停止`
<!--SR:!2022-09-09,3,250-->

#🧠 假設目前暫停在 A 行的 `double`，點擊step-into-next-function call 按鈕後會往哪裡走？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662387052/blog/debugger/browser_debugger_breakpoint_upj2ov.png) ->->-> `點擊圖示後會跳至 B 行，也就是 `double` 的第一行。`
<!--SR:!2022-09-09,3,250-->

#🧠 假設目前暫停在 A 行的 `double`，點擊step-over-next-function call 按鈕後會往哪裡走？ ->->-> ` 點擊圖示後會執行 `double` 內的所有程式碼並停在 D 行的 `console.log`。`
<!--SR:!2022-09-09,3,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@wikidataBreakpoint2022]]
[[@wikidataDuanDian2021]]
[[@ithomeDay13Sources]]
[[@chromeJavaScriptDebuggingReference]]