## 描述

> 某些受歡迎的JavaScript 函式庫的事件處理器(event handler) 相當喜愛迫使你的callback把this指向於觸發了該事件的DOM元件。遺憾的是，這些工具很少會讓你自行選擇


重點：
- JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件
- 舉例：
	- addEventListener：會將callback呼叫的this設定成發生事件的DOM節點
		- 只要是匿名函式、命名函式，皆會被系統以explicit binding設定成發生事件時的DOM節點
	- HTML DOM 標籤上所提供onxxx標籤來填入對應callback執行內容，xxx為事件名稱：會將callback呼叫的this設定成發生事件的DOM節點


### 案例1：使用HTML DOM 標籤上所提供onxxx標籤

```
<button onclick="console.log('this', this);">hi</button>
```

結果：
- 由於onclick本身就是在定義好的callback function設定其內容，所以當callback被呼叫時，就會以發生事件的dom節點為this
```
this <button onclick="console.log('this', this);">
```


### 案例2：HTML DOM 標籤上所提供onxxx標籤
```
<button onclick="(function test() {console.log('test', this)})()">hi</button>
```
結果：
- 由於onclick本身就是在定義好的callback function設定其內容，但在這裡又是在callback function進行另一個函式的呼叫，其呼叫形式會被JS解析器判定成default binding而以window來執行
```
test Window
```

### 案例3：addEventListener

```
<button id="test">hi</button>
```

```
const dom = document.getElementById('test');

dom.addEventListener('click', function test() {
  console.log('test', this)
})
```

結果：
```
test <button id="test">
```




## 複習

#🧠 JS部分函式庫所提供的事件處理器和this物件之間的關係 ->->-> `JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件`
<!--SR:!2025-01-15,510,250-->

#🧠 JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件，請舉例 ->->-> `	- addEventListener：會將callback呼叫的this設定成發生事件的DOM節點 - HTML DOM 標籤上所提供onxxx標籤來填入對應callback執行內容，xxx為事件名稱：會將callback呼叫的this設定成發生事件的DOM節點`
<!--SR:!2023-12-13,142,229-->


#🧠 JS部分函式庫所提供的事件處理器會將callback呼叫設定特定物件為this物件，通常特定物件會是DOM元件，請舉例 ->->-> `	- addEventListener：會將callback呼叫的this設定成發生事件的DOM節點 - HTML DOM 標籤上所提供onxxx標籤來填入對應callback執行內容，xxx為事件名稱：會將callback呼叫的this設定成發生事件的DOM節點`
<!--SR:!2023-12-13,142,229-->


#🧠 HTML DOM 標籤上所提供onxxx標籤和事件處理的callback有何關係？->->-> `首先在這裡已定義好事件處理的函式本身，標籤是指定其函式內容`
<!--SR:!2024-02-26,294,250-->

#🧠 addEventListener(a, callback) 中的callback若是匿名函式，其callback呼叫時的this會是什麼->->-> `會被系統以explicit binding設定成發生事件時的DOM節點`
<!--SR:!2024-11-28,473,250-->

#🧠 addEventListener(a, callback) 中的callback若是命名函式，其callback呼叫時的this會是什麼 ->->-> `會被系統以explicit binding設定成發生事件時的DOM節點`
<!--SR:!2024-12-09,473,250-->


#🧠 addEventListener(a, callback) 中的callback若是箭頭函式，其callback呼叫時的this會是什麼 ->->-> `會以箭頭函式的語彙綁定為主，並不會直接設定成發生事件的DOM節點`
<!--SR:!2024-11-16,464,250-->

#🧠 addEventListener(a, callback) 中的callback若是函式物件，其callback呼叫時的this會是什麼 ->->-> `會被系統以explicit binding設定成發生事件時的DOM節點`
<!--SR:!2024-11-19,464,250-->

#🧠 HTML上有這段\<button onclick="console.log('this', this);"\>hi\<\/button\> ，請問this會是什麼？為什麼？->->-> `button。由於onclick本身就是在定義好的callback function設定其內容，所以當callback被呼叫時，就會以發生事件的dom節點為this`
<!--SR:!2024-07-14,374,250-->

#🧠 HTML上有這段\<button onclick="(function test() \{console.log('test', this)\})()"\>hi\<\/button\> ，請問this會是什麼？為什麼？->->-> `結果為：test Window。由於onclick本身就是在定義好的callback function設定其內容，但在這裡又是在callback function進行另一個函式的呼叫，其呼叫形式會被JS解析器判定成default binding而以window來執行`
<!--SR:!2024-11-12,453,250-->

#🧠 \<button id="test"\>hi\<\/button\> dom.addEventListener('click', function test() \{   console.log('test', this) \}) 請問this會是什麼？->->-> `test <button id="test">`
<!--SR:!2024-11-15,463,250-->

#🧠 addEventListener(a, callback)中的callback得是什麼形式才會是設定發生事件時的DOM節點 ->->-> `匿名函式、命名函式`
<!--SR:!2024-11-17,444,250-->

#🧠 addEventListener(a, callback)中的callback若是箭頭函式的話，當事件發生並執行其callback的this會是什麼->->-> `會以箭頭函式的語彙綁定已經決定好的this為主`
<!--SR:!2024-06-14,344,250-->

#🧠 addEventListener(a, callback)中的callback若是匿名函式的話，當事件發生並執行其callback的this會是什麼->->-> `發生事件時的DOM節點 `
<!--SR:!2023-09-02,181,250-->

#🧠 addEventListener(a, callback)中的callback若是命名函式的話，當事件發生並執行其callback的this會是什麼->->-> `發生事件時的DOM節點 `
<!--SR:!2024-11-02,436,250-->




---
Status: #🌱 
Tags:
[[HTML]]
Links:
References: