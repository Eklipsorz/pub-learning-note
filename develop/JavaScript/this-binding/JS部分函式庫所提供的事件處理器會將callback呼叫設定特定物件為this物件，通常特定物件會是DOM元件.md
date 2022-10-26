## 描述

> 某些受歡迎的JavaScript 函式庫的事件處理器(event handler) 相當喜愛迫使你的callback把this指向於觸發了該事件的DOM元件。遺憾的是，這些工具很少會讓你自行選擇


重點：
- JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件
- 舉例：
	- addEventListener：會將callback呼叫的this設定成發生事件的DOM節點
	- HTML DOM 標籤上所提供onxxx標籤來填入對應callback執行內容，xxx為事件名稱：會將callback呼叫的this設定成發生事件的DOM節點


### 案例1
```
<button onclick="(function test() {console.log('test', this)})()">hi</button>
```

### 案例2

```
<button id="test">hi</button>
```




## 複習

#🧠 JS部分函式庫所提供的事件處理器和this物件之間的關係 ->->-> `JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件`
<!--SR:!2022-11-23,28,250-->

#🧠 JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件，請舉例 ->->-> `	- addEventListener：會將callback呼叫的this設定成發生事件的DOM節點 - HTML DOM 標籤上所提供onxxx標籤來填入對應callback執行內容，xxx為事件名稱：會將callback呼叫的this設定成發生事件的DOM節點`
<!--SR:!2022-11-23,28,250-->



---
Status: #🌱 
Tags:
[[HTML]]
Links:
References: