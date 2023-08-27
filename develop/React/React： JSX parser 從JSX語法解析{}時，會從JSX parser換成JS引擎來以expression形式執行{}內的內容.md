## 描述
[[@dsanAnswerWhatCurly2017]]
> The curly braces are a special syntax to let the JSX parser know that it needs to interpret the contents in between them as JavaScript instead of a string.
>
> You need them when you want to use a JavaScript expression like a variable or a reference inside JSX. Because if you use the standard double quote syntax like so:


```
var css = { color: red }
<h1 style="css">Hello world</h1>
```

> JSX doesn't know you meant to use the variable `css` in the style attribute instead of the string. And by placing the curly braces around the variable `css`, you are telling the parser "take the contents of the variable `css` and put them here". (Technically its evaluating the content)

> This process is generally referred to as "interpolation".


重點：
- JSX 語法本身是語法糖，包含住React原生建立 Virtual DOM & 對應 Virtual DOM的語法
- JSX 語法形式為JavaScript 和 XML 融合在一起的產物 或者 純粹 XML 
- 當解析到JSX語法就會以JSX解析器來解析，過程中解析器從JSX解析\{\}時，就會從JSX解析器更換成JavaScript引擎來負責解析內括號內容並以expression來執行
- JSX 語法中唯一能夠執行JavaScript的地方是{expression}
## 複習
#🧠 當解析到JSX語法時，會交給哪個解析器進行執行？ ->->-> `JSX parser`
<!--SR:!2024-01-09,301,250-->

#🧠 JSX 語法形式為何？ (有兩種 XML)->->-> `JavaScript 和 XML 融合在一起的產物 或者 純粹 XML `
<!--SR:!2023-11-18,83,210-->

#🧠 JSX 語法形式為何？ (有兩種)->->-> `JavaScript 和 XML 融合在一起的產物 或者 純粹 XML `
<!--SR:!2024-05-16,321,248-->


#🧠 當JSX parser從JSX語法解析到\{\}，會如何執行？->->-> `過程中解析器從JSX解析{}時，就會從JSX解析器更換成JavaScript引擎來負責解析內括號內容並以expression來執行`
<!--SR:!2025-02-22,553,250-->

#🧠 JSX 語法糖中哪個地方能夠執行JS？->->-> `JSX 語法中唯一能夠執行JavaScript的地方是{expression}、當陣列的其中一個項目、單獨回傳JS Expression`
<!--SR:!2023-08-08,189,250-->
`


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@dsanAnswerWhatCurly2017]]