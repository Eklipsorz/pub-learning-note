## 描述

https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md
> Modern JS engines actually employ numerous variations of both compilation and interpretation in the handling of JS programs.
> 
> Our conclusion there is that JS is most accurately portrayed as a **compiled language**.


https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md
> Scope is primarily determined during compilation, so understanding how compilation and execution relate is key in mastering scope.

> In classic compiler theory, a program is processed by a compiler in three basic stages:
> 
> 1.  **Tokenizing/Lexing:** breaking up a string of characters into meaningful (to the language) chunks, called tokens. For instance, consider the program: `var a = 2;`. This program would likely be broken up into the following tokens: `var`, `a`, `=`, `2`, and `;`. Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not.
    
> (The difference between tokenizing and lexing is subtle and academic, but it centers on whether or not these tokens are identified in a _stateless_ or _stateful_ way. Put simply, if the tokenizer were to invoke stateful parsing rules to figure out whether `a` should be considered a distinct token or just part of another token, _that_ would be **lexing**.)
    
> 2.  **Parsing:** taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This is called an Abstract Syntax Tree (AST).
    
> For example, the tree for `var a = 2;` might start with a top-level node called `VariableDeclaration`, with a child node called `Identifier` (whose value is `a`), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral`(whose value is `2`).
    
> 3.  **Code Generation:** taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, and other factors.
    
> The JS engine takes the just described AST for `var a = 2;` and turns it into a set of machine instructions to actually _create_ a variable called `a` (including reserving memory, etc.), and then store a value into `a`.


JavaScript 是一種具有編譯、直譯特性的程式語言，在執行之前，會先執行編譯將程式碼轉換成優化後的程式碼，最後在邊解析邊執行。

### 編譯目的
編譯的目的是確立Scope以及在短時間內轉換成最大效能的程式碼

確立Scope：
	- 會於編譯期間替var變數宣告、函式宣告分配記憶體以及給予初始值
	- 定義每個識別字所對應的變數、函式
	- 定義Execution Context

轉換成最大效能的程式碼
https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting
> 變數和函數的宣告會在編譯階段就被放入記憶體，但實際位置和程式碼中完全一樣。



編譯基本流程：
- **Tokenizing**：先將程式碼依據用途來拆分成字串來處理
> breaking up a string of characters into meaningful (to the language) chunks, called tokens

比如以下程式碼，會經過tokenizing的流程，先拆成var、a、=、2、; 這五個字串，並構成存放五個字串的陣列
```
var a = 2;	
```

-  **Parsing** ：將Tokenizing所組成的陣列依據字串間的關係來分析並組成樹狀結構，該結構為AST(Abstract Syntax Tree)，組成原因是為了更方便程式分析並轉換

比如以下程式碼
```
var a = 2;
// result
['var', 'a', '=', '2', ';']
```
一開始會以var這關鍵字作為root節點，接著它的子節點會是a這個識別字，接著在a這個節點構成另一個子節點來存放2，也就是var - a - 2。
> might start with a top-level node called `VariableDeclaration`, with a child node called `Identifier` (whose value is `a`), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral`


- **Code Generation** ：將樹狀結構轉換成對應形式的程式語言，不一定會是機械碼
實際上會比這些流程還要複雜，但會產生比先前更為有效率執行的程式碼

比如拿var - a - 2所構成的AST來轉換對應形式的代碼，那麼其代碼最後會是建立一個名為a的變數，然後分配記憶體區塊來存放2，並讓變數對應該記憶體區塊。
> The JS engine takes the just described AST for `var a = 2;` and turns it into a set of machine instructions to actually _create_ a variable called `a` (including reserving memory, etc.), and then store a value into `a`.

### compiler 命名緣由
[[@Compiler2022]] 所描述的：
> a compiler is a computer program that translates computer code written in one programming language (the source language) into another language (the target language)

重點：
- compiler 是一個電腦程式
- 主要將特定形式的程式語言轉換成另一種形式的程式語言，不一定是指從特定語言轉換成機械碼

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References:
[[@Compiler2022]]
