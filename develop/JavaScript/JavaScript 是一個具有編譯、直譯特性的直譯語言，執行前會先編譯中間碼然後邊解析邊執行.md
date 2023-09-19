## 描述

[[@simpsonYouDonKnow2022]] 所描述：
> Modern JS engines actually employ numerous variations of both compilation and interpretation in the handling of JS programs.
> 
> Our conclusion there is that JS is most accurately portrayed as a **compiled language**.


[[@simpsonYouDonKnow2022]] 所描述：
> Scope is primarily determined during compilation, so understanding how compilation and execution relate is key in mastering scope.

> In classic compiler theory, a program is processed by a compiler in three basic stages:
> 
> 1.  **Tokenizing/Lexing:** breaking up a string of characters into meaningful (to the language) chunks, called tokens. For instance, consider the program: `var a = 2;`. This program would likely be broken up into the following tokens: `var`, `a`, `=`, `2`, and `;`. Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not.
    
> (The difference between tokenizing and lexing is subtle and academic, but it centers on whether or not these tokens are identified in a _stateless_ or _stateful_ way. Put simply, if the tokenizer were to invoke stateful parsing rules to figure out whether `a` should be considered a distinct token or just part of another token, _that_ would be **lexing**.)
    
> 2.  **Parsing:** taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This is called an Abstract Syntax Tree (AST).
    
> For example, the tree for `var a = 2;` might start with a top-level node called `VariableDeclaration`, with a child node called `Identifier` (whose value is `a`), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral`(whose value is `2`).
    
> 3.  **Code Generation:** taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, and other factors.
    
> The JS engine takes the just described AST for `var a = 2;` and turns it into a set of machine instructions to actually _create_ a variable called `a` (including reserving memory, etc.), and then store a value into `a`.

> 若以有點循環的方式來定義它，語彙範疇(lexical scope)就是在語彙分析時期(lexing time)定義的範疇。換句話說，語彙範疇取決於變數與區塊的範疇是由你，在寫作時期，於何處編寫的，所以(在多數情況下)lexer(語彙分析器)處理你的程式碼時，就已經寫定


> lexing(語彙分析，即tokenizing，語法基本單元化)，檢視一連串的原始碼字元，並指定語義(semantic meaning)給那些語法基本單元(tokens)作為某些有狀態的分析動作之結果

JavaScript 是一種具有編譯、直譯特性的直譯程式語言，在執行之前，會先執行編譯將程式碼轉換成優化後的程式碼，最後在邊解析邊執行。

### 編譯目的
編譯的目的是確立Scope以及在短時間內轉換成最大效能的程式碼

確立Scope：
	- 會替var變數宣告、函式宣告分配記憶體以及給予初始值
	- 定義每個識別字所對應的變數、函式
	- 定義Execution Context
	[[JavaScript 會在編譯時期產出對應的bytecode，而對應bytecode功能會是分配記憶體給函式宣告、var宣告、定義各種scope的execution context]]
轉換成最大效能的程式碼
[[@mdnTiShengHoistingShuYuBiao]]
> 變數和函數的宣告會在編譯階段就被放入記憶體，但實際位置和程式碼中完全一樣。

編譯基本流程：
- **Tokenizing**：先將程式碼依據用途來拆分成字串來處理，通常會按照空白當間隔來取
> breaking up a string of characters into meaningful (to the language) chunks, called tokens

比如以下程式碼，會經過tokenizing的流程，先拆成var、a、=、2、; 這五個字串，並構成存放五個字串的陣列
```
var a = 2;	
```

-  **Parsing** ：將Tokenizing所組成的陣列依據程式語言所定義的語義和語法規則來將陣列的字串組裝合法的語意和語法，若合法就會構成樹狀結構，該結構為AST(Abstract Syntax Tree)；若不會就報錯，樹狀的組成原因是為了更方便程式分析並轉換
[[JavaScript Parsing中所要做的事情就是將tokenizing得到字串陣列轉換成代表合法句子的樹狀結構以及賦予其樹狀結構一些語意上的性質]]
比如以下程式碼
```
var a = 2;
// result
['var', 'a', '=', '2', ';']
```
一開始會以var這關鍵字作為root節點，接著它的子節點會是a這個識別字，接著在a這個節點構成另一個子節點來存放2，也就是var - a - 2。
> might start with a top-level node called `VariableDeclaration`, with a child node called `Identifier` (whose value is `a`), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral`

- **Code Generation** ：將樹狀結構轉換成對應形式的程式語言，不一定會是機械碼，很有可能會是比先前更為效率執行的程式碼，介於JS和機械碼之間的ByteCode

p.s. 實際上會比這些流程還要複雜，但會產生比先前更為有效率執行的程式碼

比如拿var - a - 2所構成的AST來轉換對應形式的代碼，那麼其代碼最後會是建立一個名為a的變數，然後分配記憶體區塊來存放2，並讓變數對應該記憶體區塊。
> The JS engine takes the just described AST for `var a = 2;` and turns it into a set of machine instructions to actually _create_ a variable called `a` (including reserving memory, etc.), and then store a value into `a`.

### 編譯期間：函式宣告和var變數宣告會發生什麼
替函式宣告和var變數宣告分配了記憶體區塊給他們，並定義其初始值，函式部分的記憶體區塊是存放著函式內容，var變數部分的記憶體區塊是存放著undefined

### 編譯期間：const/let變數宣告會發生什麼
編譯期間並不會分配記憶體給他們，也不會分配初始值

### 編譯和執行的時機
- 當開始執行特定JS檔案時，就會進入針對各種Scope下的內容進行編譯
[[JavaScript 會在編譯時期產出對應的bytecode，而對應bytecode功能會是分配記憶體給函式宣告、var宣告、定義各種scope的execution context]]

### compiler 命名緣由
[[@Compiler2022]] 所描述的：
> a compiler is a computer program that translates computer code written in one programming language (the source language) into another language (the target language)

重點：
- compiler 是一個電腦程式
- 主要將特定形式的程式語言轉換成另一種形式的程式語言，不一定是指從特定語言轉換成機械碼

### interpreter 命名緣由
[[@JavaScriptBianYiYuanLiYuYuYanJingCuiZhiHu]] 所描述：
> 实际上很多解释器内部是以“编译器+虚拟机”的方式来实现的，先通过编译器将源码转换为AST或者字节码，然后由虚拟机去完成实际的执行。 
> 
> 解释器中的编译器的输出可能是AST，也可能是字节码之类的指令序列；一般会把执行后者的程序称为VM，而执行前者的还是笼统称为解释器或者树遍历式解释器（tree-walking interpreter）。这只是种习惯而已，并没有多少确凿的依据。只不过线性（相对于树形）的指令序列看起来更像一般真正机器会执行的指令序列而已。
> 
>所以编译器是把一种语言翻译成另一种语言，而解释器要承担编译器的全部责任，同时还要把编译出来的东西去执行。因此解释器 = 编译 + 执行，而编译器只负责其中编译的部分。因此如果实现出解释器再把它变成编译器是没有问题的，反过来则不行。

解釋器
> an interpreter is a computer program that directly executes instructions written in a programming or scripting language, without requiring them previously to have been compiled into a machine language program.

> 是一種電腦程式，能夠把直譯語言直接轉譯執行。直譯器就像一位「中間人」。直譯器邊直接轉譯邊執行，因此依賴於直譯器的程式執行速度比較緩慢

> An interpreter generally uses one of the following strategies for program execution:
> 
> 1. Parse the source code and perform its behavior directly;
> 2. Translate source code into some efficient intermediate representation or object code and immediately execute that;
> 3. Explicitly execute stored precompiled bytecode made by a compiler and matched with the interpreter Virtual Machine.

重點：
- 解釋器是一個電腦程式，主要會邊將原始碼轉換成可直接執行的程式碼形式邊執行，總而言之，就是編譯＋執行
- 具體實現方式為：
	- 以編譯器＋虛擬機為主的解釋器：先將程式碼轉換成AST或者ByteCode，然後再將AST或者ByteCode丟至虛擬機執行

執行策略如下：
	- 直接解析原始碼並執行：直接將原始碼丟進虛擬機/解釋器來邊轉換機械碼邊執行
	- 將原始碼先轉換成成中間碼(ByteCode)並立即執行：將原始碼丟進編譯器轉換中間碼(介於原始碼和機械碼之間，並且只有虛擬機能解析的形式)，並存放在記憶體或者緩存，接著丟進虛擬機邊轉換機械碼邊執行
	- 先透過compiler將所有的原始碼編譯成中間碼，接著再丟進interpreter轉換成機械碼並立即執行：將中間碼丟進編譯器轉換成機械碼，並存放在記憶體或者緩存，接著丟進虛擬機執行

解釋器和編譯器之間的差別：
	- 解釋器是負責編譯＋執行
	- 編譯器是負責編譯


## 複習
#🧠 compiler 是什麼->->-> `是一個電腦程式，主要將特定形式的程式語言轉換成另一種形式的程式語言`
<!--SR:!2025-02-07,563,249-->

#🧠 compiler 轉換後的程式語言形式會是機械碼嗎？->->-> `不一定`
<!--SR:!2023-12-15,108,209-->

#🧠 interpreter 是什麼？ ->->-> `解釋器是一個電腦程式，主要會邊將原始碼轉換成可直接執行的程式碼形式邊執行，總而言之，就是編譯＋執行`
<!--SR:!2024-11-14,503,250-->

#🧠 interpreter 與 compiler 相比，差別是什麼？ ->->-> `interpreter 是負責編譯和執行，而compiler是只負責編譯`
<!--SR:!2024-07-29,432,250-->

#🧠 interpreter 具體的執行策略有哪些？ ->->-> `	- 直接解析原始碼並執行：直接將原始碼丟進虛擬機/解釋器來邊轉換機械碼邊執行 - 將原始碼先轉換成成中間碼(ByteCode)並立即執行：將原始碼丟進編譯器轉換中間碼(介於原始碼和機械碼之間，並且只有虛擬機能解析的形式)，並存放在記憶體或者緩存，接著丟進虛擬機邊轉換機械碼邊執行 - 先透過compiler將所有的原始碼編譯成中間碼，接著再丟進interpreter轉換成機械碼並立即執行：將中間碼丟進編譯器轉換成機械碼，並存放在記憶體或者緩存，接著丟進虛擬機執行`
<!--SR:!2023-12-26,105,210-->

#🧠 (重複) interpreter 具體的執行策略有哪些？ ->->-> `	- 直接解析原始碼並執行：直接將原始碼丟進虛擬機/解釋器來邊轉換機械碼邊執行 - 將原始碼先轉換成成中間碼(ByteCode)並立即執行：將原始碼丟進編譯器轉換中間碼(介於原始碼和機械碼之間，並且只有虛擬機能解析的形式)，並存放在記憶體或者緩存，接著丟進虛擬機邊轉換機械碼邊執行 - 先透過compiler將所有的原始碼編譯成中間碼，接著再丟進interpreter轉換成機械碼並立即執行：將中間碼丟進編譯器轉換成機械碼，並存放在記憶體或者緩存，接著丟進虛擬機執行`
<!--SR:!2023-10-24,35,225-->


#🧠 interpreter 通常會由什麼元件組成？ 分別做什麼->->-> `編譯器＋虛擬機，編譯器負責將原始碼編譯成只有虛擬機能解析的語言形式，如bytecode或者machine code，並且將該語言交給虛擬機邊轉換機械碼邊執行`
<!--SR:!2025-03-08,580,249-->

#🧠 interpreter的編譯器能將原始碼編譯成什麼？ ->->-> `ByteCode 或者 Machine Code`
<!--SR:!2024-01-16,128,229-->

#🧠 JavaScript 是什麼樣特性的語言？編譯特性？直譯特性？ ->->-> `同時擁有編譯和直譯特性的程式語言`
<!--SR:!2024-04-02,375,250-->

#🧠 除了產生的中間碼以外，JavaScript 編譯後，函式宣告和var變數宣告發生了什麼->->-> `替函式宣告和var變數宣告分配了記憶體區塊給他們，並定義其初始值，函式部分的記憶體區塊是存放著函式內容，var變數部分的記憶體區塊是存放著undefined`
<!--SR:!2025-02-12,567,249-->

#🧠 除了產生的中間碼以外，JavaScript 編譯後，const/let變數宣告發生了什麼->->-> `不會分配記憶體給這些識別字，更不會分配初始值給他們`
<!--SR:!2024-11-06,503,249-->


#🧠 JavaScript 會是編譯和執行嗎？還是直接執行 ->->-> `是編譯和執行`
<!--SR:!2023-10-30,279,250-->

#🧠 JavaScript 的 編譯和執行之間的流程具體是什麼？ 以及EC?(先不考慮JIT) ->->-> `會先將每行程式碼轉換成多個字串所構成的陣列，接著透過parsing將陣列中的字串試著組裝代表合法expression、declaration、statement的樹狀結構，依據樹狀結構來生成對應的bytecode並存在記憶體，過程中會分配記憶體給var變數宣告和函式宣告，建立EC，最後編譯完對應的bytecode，便直接丟進虛擬機或者負責邊解析邊執行的元件來執行`
<!--SR:!2024-02-24,351,250-->

#🧠 JavaScript 的 編譯後的語言形式會是什麼 ->->-> `介於原始碼和機械碼之間的程式語言，只有虛擬機/引擎能夠解析執行的語言`
<!--SR:!2024-03-27,370,250-->

#🧠 JavaScript 的編譯目的是什麼？ ->->-> `確定每個識別字的scope和轉換成最大效能的程式碼`
<!--SR:!2023-12-03,152,229-->


#🧠 JavaScript 一編譯完成後的bytecode會做到哪些事情， ->->-> `會於編譯期間替var變數宣告、函式宣告分配記憶體以及給予初始值、定義每個識別字所對應的變數和函式、定義Execution Context、引擎能夠執行最大效能的程式碼`
<!--SR:!2024-08-09,461,250-->

#🧠 拿var a = 2 來說明一下編譯的流程，以基本的三個步驟來說起﹔tokenizing -> parsing -> code generation ->->-> `會經過tokenizing的流程，先拆成var、a、=、2、; 這五個字串並賦予特定狀態來表示誰是關鍵字、誰是變數、誰是指派值，並構成存放五個字串的陣列，接著透過陣列來轉換成樹狀，一開始會以var這關鍵字作為root節點，接著它的子節點會是a這個識別字，接著在a這個節點構成另一個子節點來存放2，也就是var - a - 2，將樹狀結構轉換成對應形式的程式語言，不一定會是機械碼，很有可能會是比先前更為效率執行的程式碼，如JS碼、介於JS和機械碼之間的ByteCode`
<!--SR:!2024-02-25,214,230-->


#🧠 JavaScript 編譯中的**Tokenizing**是什麼？ ->->-> `先將程式碼依據用途來拆分成字串來處理，通常會按照空白當間隔來取`
<!--SR:!2023-11-15,113,229-->

#🧠 JavaScript 編譯中的**Parsing**是什麼？->->-> `將Tokenizing所組成的陣列依據程式語言所定義的語義和語法規則來將陣列的字串組裝合法的語意和語法，若合法就會構成樹狀結構，該結構為AST(Abstract Syntax Tree)；若不會就報錯，樹狀的組成原因是為了更方便程式分析並轉換`
<!--SR:!2025-02-03,559,249-->

#🧠 JavaScript 編譯中的**Code Generation** 是什麼？ ->->-> `將樹狀結構轉換成對應形式的程式語言，不一定會是機械碼，很有可能會是比先前更為效率執行的程式碼，如JS碼、介於JS和機械碼之間的ByteCode`
<!--SR:!2024-01-19,333,250-->


#🧠 JavaScript 的 編譯和執行是何時觸發？會不會編譯全部種類scope下的內容？->->-> `當開始執行特定JS檔案時，就會進入針對各種Scope下的內容進行編譯`
<!--SR:!2023-11-13,111,229-->



---
Status: #🌱 
Tags:
[[JavaScript]] - Scope
Links:
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
[[Scope 是指某識別字對應特定實體的合法使用範圍，具體實現Scope的方式有Lexical Scope 和Dynam Scope]]
[[Just-In-Time Compilation 是指特定代碼需要執行時才進行機械碼的編譯，接著將機械碼存放在緩存來執行]]
[[JavaScript Parsing中所要做的事情就是將tokenizing得到字串陣列轉換成代表合法句子的樹狀結構以及賦予其樹狀結構一些語意上的性質]]
References:
[[@Compiler2022]]
[[@simpsonYouDonKnow2022]]
[[@mdnTiShengHoistingShuYuBiao]]
[[@JavaScriptBianYiYuanLiYuYuYanJingCuiZhiHu]]