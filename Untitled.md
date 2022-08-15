## 描述
[[@benmccormickWhyJavascriptEvent]]
> ### Inline JS
> When you do an inline onclick handler like that, you're assigning a Javascript expression to run. So you need to execute the function.
> The expression could just as easily be `onclick="handler();alert(2)"` in which case its obvious that the function needs to be called, just like it would be if it were run from a javascript file.

[[@HowDoesInline]] 
> Inline JavaScript can be achieved by using **Script tag** inside the body of the HTML, and instead of specifying the source(src=”…”) of the JavaScript file in the Script tag, we have to **write all the JavaScript code inside the Script tag**.

[[@fanyinJsZhongHehtmlZhongonclickBangDingHanShuYaoBuYaoJiaGuaHaoDeWenTiSmilFanYin]]
```
<!--方式一-->
<div onclick="fun1();fun2('world!');"></div>
```

> 那为什么DOM0方式一中却有括号呢？那是因为标签的事件属性里引号之间会被当做js语句直接执行，加了括号才能保证调用并执行函数。但是由于是用元素标签这种方式绑定的事件，执行的时机就被控制在了点击该标签时触发。

重點：
- inline javascript 是指JavaScript被包含在HTML文件內部，而非以獨立的JS檔案與HTML檔案分開
- inline javascript 的事件綁定對應函式會是字串，當被瀏覽器解析到onXXXX (XXXX 是指事件綁定)時，會將執行權給JS引擎來處理，JS引擎實際上**會是指定該元件上的對應事件發生時要執行什麼指令，而非設定函式位址來方便呼叫哪個函式來作為對應事件的事件處理**

- 舉例來說，以下的onclick只要經由瀏覽器的JS引擎解析，就是告知引擎發生點擊事件時就執行function()，當然你設定function，就是會執行function
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
[[@fanyinJsZhongHehtmlZhongonclickBangDingHanShuYaoBuYaoJiaGuaHaoDeWenTiSmilFanYin]]