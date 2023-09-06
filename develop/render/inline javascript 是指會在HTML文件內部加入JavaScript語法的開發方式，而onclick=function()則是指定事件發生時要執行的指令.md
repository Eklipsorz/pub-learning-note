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
- inline javascript 是指會在夾雜其他內容的文件加入JavaScript語法的開發方式，而非以獨立的JS檔案與HTML檔案分開，文件通常是HTML
- inline javascript ：HTML元件上的事件綁定屬性對應函式會是字串，當被瀏覽器解析到onXXXX (XXXX 是指事件綁定)時，會將執行權給JS引擎來處理，JS引擎實際上**會是指定該元件上的對應事件發生時要執行什麼指令，而非設定函式位址來方便呼叫哪個函式來作為對應事件的事件處理**
- 總結來說，替該div元件設定點擊事件發生時就直接執行code，事件發生時就執行code
```
<div onclick="<code>"> </div>
```
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

#🧠 inline 命名緣由？ ->->-> `inline 是被包含在其他資訊上的 或者 排成一條線的`
<!--SR:!2023-12-21,124,170-->


#🧠 inline javascript 是什麼？ ->->-> `指會在夾雜其他內容的文件加入JavaScript語法的開發方式`
<!--SR:!2024-05-04,380,250-->

#🧠 inline javascript 是指會在夾雜其他內容的文件加入JavaScript語法的開發方式，那麼文件通常會是指？ 整體組合在一起就是？->->-> `HTML，inline javascript 是指會在HTML文件內部加入JavaScript語法的開發方式`
<!--SR:!2023-11-30,284,250-->

#🧠 在HTML 文件上直接以JS來設定事件綁定的開發方式叫做什麼 ->->-> `inline javascript`
<!--SR:!2023-12-23,107,229-->


#🧠 inline javascript 和檔案分離之間的差別->->-> `前者指會在夾雜其他內容的文件加入JavaScript語法的開發方式；後者則是按照內容種類來分檔案來開發，其中一個為專門存放JavaScript的檔案`
<!--SR:!2023-12-02,99,230-->

#🧠 HTML元件上的事件綁定屬性對應函式會是？ ->->-> `用字串來表達函式呼叫`
<!--SR:!2025-03-30,587,250-->


#🧠  為什麼\<div onclick="function();"\> \<\/div\>的function要加括號？->->-> `當被瀏覽器解析到onXXXX (XXXX 是指事件綁定)時，會將執行權給JS引擎來處理，JS引擎實際上**會是指定該元件上的對應事件發生時要執行什麼指令，而非設定函式位址來方便呼叫哪個函式來作為對應事件的事件處理**，而當事件發生時，就會直接直接對應指令-function()`
<!--SR:!2024-01-05,304,250-->

#🧠 具體來說onclick會是設定什麼？\<div onclick="\<code\>"\> \<\/div\> ->->-> `替該div元件設定點擊事件發生時就直接執行code，事件發生時就執行code`
<!--SR:!2024-07-02,414,250-->

#🧠 HTML DOM：請用div元件和事件綁定屬性來設定點擊事件處理，處理會是以function來替代 ->->-> `<div onclick="function();"> </div>`
<!--SR:!2024-07-28,431,250-->

#🧠 解釋一下瀏覽器和JS引擎如何處理？ \<div onclick="function();"\> \<\/div\> ->->-> `只要經由瀏覽器的JS引擎解析，就是告知引擎發生點擊事件時就執行function()`
<!--SR:!2024-06-17,406,250-->

#🧠 \<div onclick="function();"\> \<\/div\> 和 \<div onclick="function"\> \<\/div\> 這兩者有啥差別->->-> `前者是事件發生時就執行function()；後者則是事件發生時就執行function`
<!--SR:!2024-07-02,316,230-->

---
Status: #🌱 
Tags:
 [[JavaScript]]
Links:
References:
[[@benmccormickWhyJavascriptEvent]]
[[@HowDoesInline]]
[[@fanyinJsZhongHehtmlZhongonclickBangDingHanShuYaoBuYaoJiaGuaHaoDeWenTiSmilFanYin]]