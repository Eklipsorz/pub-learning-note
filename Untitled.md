## 描述
[[@benmccormickWhyJavascriptEvent]]
> ### Inline JS
> When you do an inline onclick handler like that, you're assigning a Javascript expression to run. So you need to execute the function.
> The expression could just as easily be `onclick="handler();alert(2)"` in which case its obvious that the function needs to be called, just like it would be if it were run from a javascript file.

[[@HowDoesInline]] 
> Inline JavaScript can be achieved by using **Script tag** inside the body of the HTML, and instead of specifying the source(src=”…”) of the JavaScript file in the Script tag, we have to **write all the JavaScript code inside the Script tag**.

重點：
- inline javascript 是指JavaScript被包含在HTML文件內部，而非以獨立的JS檔案與HTML檔案分開
- inline javascript 的事件綁定對應函式會是字串，當被瀏覽器解析到onXXXX (XXXX 是指事件綁定)時，會將執行權給JS引擎來處理，JS引擎會先透過執行function();來得到對應函式的內容並與該綁定元件上的特定事件綁定其函式內容，當事件發生時，就以該函式的內容來執行，細節：
	- 在這裡function()並非是指在被JS引擎解析時就執行內部的東西
```
<div onclick="function();"> </div>
```
### inline 命名緣由
inline ：
> included as part of the main text on a page, rather than in a separate section

> with parts arranged in a line


重點：
- inline 是被包含在其他資訊上的 或者 排成一條線的

## 複習

#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@benmccormickWhyJavascriptEvent]]
[[@HowDoesInline]]