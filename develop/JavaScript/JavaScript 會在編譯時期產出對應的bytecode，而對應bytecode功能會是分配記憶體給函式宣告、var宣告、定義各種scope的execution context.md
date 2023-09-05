## 描述

[[@simpsonYouDonKnow2022]] 描述的：
> ## Marbles, and Buckets, and Bubbles... Oh My!

> One metaphor I've found effective in understanding scope is sorting colored marbles into buckets of their matching color.

> Imagine you come across a pile of marbles, and notice that all the marbles are colored red, blue, or green. Let's sort all the marbles, dropping the red ones into a red bucket, green into a green bucket, and blue into a blue bucket. After sorting, when you later need a green marble, you already know the green bucket is where to go to get it.

> In this metaphor, the marbles are the variables in our program. The buckets are scopes (functions and blocks), which we just conceptually assign individual colors for our discussion purposes. The color of each marble is thus determined by which _color_ scope we find the marble originally created in.

> Let's annotate the running program example from Chapter 1 with scope color labels:

```
// outer/global scope: RED

var students = [
    { id: 14, name: "Kyle" },
    { id: 73, name: "Suzy" },
    { id: 112, name: "Frank" },
    { id: 6, name: "Sarah" }
];

function getStudentName(studentID) {
    // function scope: BLUE

    for (let student of students) {
        // loop scope: GREEN

        if (student.id == studentID) {
            return student.name;
        }
    }
}

var nextStudent = getStudentName(73);
console.log(nextStudent);   // Suzy
```




> We've designated three scope colors with code comments: RED (outermost global scope), BLUE (scope of function `getStudentName(..)`), and GREEN (scope of/inside the `for` loop). But it still may be difficult to recognize the boundaries of these scope buckets when looking at a code listing.

> Figure 2 helps visualize the boundaries of the scopes by drawing colored bubbles (aka, buckets) around each:

![](https://github.com/getify/You-Dont-Know-JS/raw/2nd-ed/scope-closures/images/fig2.png)

_Fig. 2: Colored Scope Bubbles_

> 1.  **Bubble 1** (RED) encompasses the global scope, which holds three identifiers/variables: `students` (line 1), `getStudentName` (line 8), and `nextStudent` (line 16).
> 
> 2.  **Bubble 2** (BLUE) encompasses the scope of the function `getStudentName(..)` (line 8), which holds just one identifier/variable: the parameter `studentID` (line 8).
> 
> 3.  **Bubble 3** (GREEN) encompasses the scope of the `for`-loop (line 9), which holds just one identifier/variable: `student` (line 9).


> Scope bubbles are determined during compilation based on where the functions/blocks of scope are written, the nesting inside each other, and so on. Each scope bubble is entirely contained within its parent scope bubble—a scope is never partially in two different outer scopes.

> Each marble (variable/identifier) is colored based on which bubble (bucket) it's declared in, not the color of the scope it may be accessed from (e.g., `students` on line 9 and `studentID` on line 10).


[[@ithomeDay14YDKJSScope]] 所描述：
> ## 技術總結

> 1.  這個第一次 parser 的階段， compiler 只在乎 Identifier。
> 2.  parser 完成就配對完成所有的 Scope， 此時 `line 10` 知道是 block Scope （綠色）。    ![](https://i.imgur.com/dvoWJeX.png)
> 3.  所有的 lexically scoped language （像是 JavaScript）， 決定所有的 `lexical scopes` and `identifiers` 在 `compile time` ，  而`不是 run time 決定` 。
> 4.  此時所有 `var let const` 之類的 Declaration 全部沒有意義，會移除，我們已經知道 Scope 規劃了。
> 5.  run time 會使用我們決定好的 lexically scoped 並產生 bytecode，也就是大家熟悉的 interpreter JavaScript 。

重點：
- JavaScript 在編譯時期主要會產出對應的bytecode，其bytecode功能會是：
	- 分配記憶體給所有函式宣告、var變數宣告並賦予初始值：函式宣告會拿到存有函式內容的記憶體區塊，var變數宣告會拿到存有undefined的記憶體區塊
	- 不分配記憶體給const/let變數宣告
	- 設定this binding
	- 設定outer reference
	- 設定在scope下為每個識別字而對應的實體物件
- 所有lexically scoped language 會在編譯時期決定lexical scopes和對應的lexical identifiers


## 複習
#🧠 JavaScript 編譯時期會生成對應ByteCode以外，其bytecode的功能會是>->-> `	- 分配記憶體給所有函式宣告、var變數宣告並賦予初始值：函式宣告會拿到存有函式內容的記憶體區塊，var變數宣告會拿到存有undefined的記憶體區塊- 不分配記憶體給const/let變數宣告 - 設定this binding  - 設定outer reference - 設定在scope下為每個識別字而對應的實體物件`




#🧠 JavaScript 編譯的bytecode會分配記憶體const/let變數宣告嗎？->->-> `不分配記憶體給const/let變數宣告`
<!--SR:!2025-01-05,495,247-->


 #🧠 JavaScript 編譯的bytecode會分配記憶體var變數/函式宣告嗎？->->-> `分配記憶體給var變數和函式宣告`
<!--SR:!2023-12-03,258,247-->


#🧠 JavaScript 什麼時候生成對應的GEC和FEC？（具體說明) ->->-> `執行階段中，快要執行GEC對應的scope才會執行對應的bytecode來生成對應EC，而FEC則是快要執行FEC對應的scope才會執行對行對應的bytecode來生成對應的FEC`
<!--SR:!2023-12-08,262,247-->



#🧠 lexically scoped language 在編譯時期會做些什麼？ (scope、生成)->->-> `確定所有種類的lexical scope 和 生成對應的ByteCode`
<!--SR:!2023-09-27,21,168-->

---
Status: #🌱 
Tags: 
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
References:
[[@simpsonYouDonKnow2022]]
[[@ithomeDay14YDKJSScope]]