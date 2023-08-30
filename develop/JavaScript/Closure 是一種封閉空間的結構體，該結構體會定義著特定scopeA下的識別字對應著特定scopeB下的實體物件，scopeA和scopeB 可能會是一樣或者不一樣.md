
## 描述

### closure 在電腦語言下的意思
> 是在支援頭等函式的程式語言中實現詞法繫結的一種技術。閉包在實現上是一個結構體，它儲存了一個函式（通常是其入口位址）和一個關聯的環境（相當於一個符號尋找表）。環境裡是若干對符號和值的對應關係，它既要包括約束變數（該函式內部繫結的符號），也要包括自由變數（在函式外部定義但在函式內被參照），有些函式也可能沒有自由變數。閉包跟函式最大的不同在於，當捕捉閉包的時候，它的自由變數會在捕捉時被確定，這樣即便脫離了捕捉時的上下文，它也能照常執行。捕捉時對於值的處理可以是值拷貝，也可以是名稱參照，這通常由語言設計者決定，也可能由使用者自行指定（如C++）。

> Closure is a behavior of functions and only functions. If you aren't dealing with a function, closure does not apply. An object cannot have closure, nor does a class have closure (though its functions/methods might). Only functions have closure.

重點：
- 除了函式以外，就只有function能夠構築closure


1. 在程式上，是一種多個scope層級之間的對應關係上的封閉空間
2. 換言之，封閉空間內的每個元素將會是特定scopeA下的識別字 和 特定scope B 的實體物件之間的對應關係，**在這裡的scope A和scope B 可能會是不一樣的或者可能會是一樣**，而識別字可對應到scope B下的實體物件
3. 具體用途為：
	- 以載入結構體的形式來允許程式碼能夠調用其他scope下的實體物件
4.  該概念會時常運用函式B能回傳函式A的情況下，其函式A會因而成為函式物件，函式物件A的scope 會是上述的scope A，函式B的scope 會是上述的scope B，並且以scope A 為主來構築closure結構體或者集合，裡頭的元素會是多個scope A識別字和對應實體物件，這些scope A識別字部分對應著scope B的實體物件，部分對應著scope A的實體物件，且為了能讓**函式物件A繼續使用著函式B的實體物件，而允許即使函式B的EC要被釋放掉的情況下，還是會在具體實現上盡可能保留著函式A還會用到的函式B的實體物件**
> A closure is a function having access to the parent scope, even after the parent function has closed.

[[@BiBaoJiSuanJiKeXue2022]] 所描述的
> 閉包和匿名函式經常被用作同義詞。但嚴格來說，匿名函式就是字面意義上沒有被賦予名稱的函式，而閉包則實際上是一個函式的實例，也就是說它是存在於記憶體里的某個結構體。

5. 該概念會運用在函式B能回傳函式A的情況下，可以使：
	- 讓函式A擁有屬於自己的變數來存取和操作
	- 打造成模組，並將function scope作為module scope來讓function回傳的function擁有module專有的變數

總結來說的話：
- 每個函式物件A會具備closure結構體，其結構體會儲存每個函式物件A所用到的識別字以及對應的實體物件，該實體物件會是在函式物件A存在的實體物件或者函式B所存在的實體物件
- 若closure中的識別字對應著包含著函式物件A的函式B所擁有的實體物件時，會為了讓closure正常使用，而保留函式B的部分EC資訊，其資訊具會是函式物件A所用到的對應實體物件
- 至於函式B的EC資訊釋放則是看目前情況是否還滿足Garbage collector所依據的保留機制-若實體物件還繼續被參照使用的話，就會保留其記憶體，直到沒被使用，到時就會釋放


### 支援運用在函式A和包含函式A的函式B的closure之程式語言是？
具體必須是能夠支援first-class function的程式語言，如JavaScript
[[first-class citizen 為一種實體，可以在特定程式語言下被當作是物件或值來看待，並且可以用物件和值所支援的操作來將實體和其他物件或值進行處理]]


### 運用在函式A和包含函式A的函式B的closure ：garbage collector

在JS中，garbage collector 由於會觀察每個記憶體區塊被使用的情況來釋放，若確定記憶體區塊後續未被使用就會釋放；反之，若確定記憶體區塊後續還會被使用就會繼續保留。

如何判定後續是否會繼續被使用：
- 編譯時來查看是否後續會被使用
- 執行時根據演算法來確定


所以當透過baz 來接收foo()所回傳的函式物件時，並且以該函式物件來呼叫時，而函式物件本身使用著foo下的a所對應的實體物件，理論上只要呼叫完foo，foo內的記憶體區塊將會被釋放，換言之，a也會被釋放，所以baz所印出的a會報錯，但實際上是可以印出2。


而這是因為函式宣告肯定會從編譯時期就分配記憶體以及查看每個識別字對應的實體物件是否後續有被使用，在這裏可以由於可從編譯時期確定後續會呼叫bar()，而bar會使用著foo下的a對應的對應實體物件，所以garbage collector確定後續會使用，所以不會釋放掉foo下的a對應的實體物件，**但就是沒釋放掉a對應的實體物件**，因而讓呼叫baz()時還能印出foo下的a的實體物件
```
function foo() {
	var a = 2;

	function bar() {
		console.log(a)
	}

	return bar
}

var baz = foo()
baz()
```


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658653407/blog/javascript/closure/You_Don_t_Know_JS_Yet-Closure2_xo614o.jpg)


### 觀察：運用在函式A和包含函式A的函式B的closure 

> For closure to be observed, a function must be invoked, and specifically it must be invoked in a different branch of the scope chain from where it was originally defined. A function executing in the same scope it was defined would not exhibit any observably different behavior with or without closure being possible; by the observational perspective and definition, that is not closure.
> 
> Let's look at some code, annotated with its relevant scope bubble colors (see Chapter 2):
> 
> The first thing to notice about this code is that the `lookupStudent(..)` outer function creates and returns an inner function called `greetStudent(..)`. `lookupStudent(..)` is called twice, producing two separate instances of its inner `greetStudent(..)` function, both of which are saved into the `chosenStudents` array.

```
// outer/global scope: RED(1)

function lookupStudent(studentID) {
    // function scope: BLUE(2)

    var students = [
        { id: 14, name: "Kyle" },
        { id: 73, name: "Suzy" },
        { id: 112, name: "Frank" },
        { id: 6, name: "Sarah" }
    ];

    return function greetStudent(greeting){
        // function scope: GREEN(3)

        var student = students.find(
            student => student.id == studentID
        );

        return `${ greeting }, ${ student.name }!`;
    };
}

var chosenStudents = [
    lookupStudent(6),
    lookupStudent(112)
];

// accessing the function's name:
chosenStudents[0].name;
// greetStudent

chosenStudents[0]("Hello");
// Hello, Sarah!

chosenStudents[1]("Howdy");
// Howdy, Frank!
```

> We verify that's the case by checking the `.name` property of the returned function saved in `chosenStudents[0]`, and it's indeed an instance of the inner `greetStudent(..)`.
> 
> After each call to `lookupStudent(..)` finishes, it would seem like all its inner variables would be discarded and GC'd (garbage collected). The inner function is the only thing that seems to be returned and preserved. But here's where the behavior differs in ways we can start to observe.
> 
> While `greetStudent(..)` does receive a single argument as the parameter named `greeting`, it also makes reference to both `students` and `studentID`, identifiers which come from the enclosing scope of `lookupStudent(..)`. Each of those references from the inner function to the variable in an outer scope is called a _closure_. In academic terms, each instance of `greetStudent(..)` _closes over_ the outer variables `students` and `studentID`.


> So what do those closures do here, in a concrete, observable sense?
> 
> Closure allows `greetStudent(..)` to continue to access those outer variables even after the outer scope is finished (when each call to `lookupStudent(..)` completes). Instead of the instances of `students` and `studentID` being GC'd, they stay around in memory. At a later time when either instance of the `greetStudent(..)` function is invoked, those variables are still there, holding their current values.
> 
> If JS functions did not have closure, the completion of each `lookupStudent(..)` call would immediately tear down its scope and GC the `students` and `studentID` variables. When we later called one of the `greetStudent(..)` functions, what would then happen?
> 
> If `greetStudent(..)` tried to access what it thought was a BLUE(2) marble, but that marble did not actually exist (anymore), the reasonable assumption is we should get a `ReferenceError`, right?
> 
> But we don't get an error. The fact that the execution of `chosenStudents[0]("Hello")` works and returns us the message "Hello, Sarah!", means it was still able to access the `students` and `studentID` variables. This is a direct observation of closure!


重點：
- 每一個lookupStudent 函式會回傳一個greetStudent這函式物件，
- 每個greetStudent由於是在被其他函式包含，所以會在編譯期間建立closure，來替每個識別字找到對應實體，除了students 和 studentId 這兩個識別字並不是greetStudent有的識別字，所以會根據scope chain往上尋找對應著包含greetStudent的函式所擁有的students 和 studentID
- 而students 和 studentID並不會因為每次lookupStudent呼叫完畢才被釋放，而是因為能夠在編譯期間判定呼叫完畢後還會被使用，因此即使lookupStudent呼叫完畢，也會在使用的人還未結束執行會保留students 和 studentID



### Closure 命名緣由
[[@simpsonYouDonKnow2022]] 所描述：
>  Closure is originally a mathematical concept, from lambda calculus. But I'm not going to list out math formulas or use a bunch of notation and jargon to define it.

1. 從數學概念-Closure衍伸過來的術語，意為著包含著特定物件的封閉空間


閉包可以用來在一個函式與一組「私有」變數之間建立關聯關係
https://zh.m.wikipedia.org/zh-tw/闭包_(计算机科学)



## 複習
#🧠 closure 命名緣由為何？ ->->-> `Closure衍伸過來的術語，意為著包含著特定物件的封閉空間`
<!--SR:!2024-12-10,526,250-->


#🧠 在程式上，closure是什麼樣的概念? ->->-> `是一種多個scope層級之間的對應關係上的封閉空間，具體會是一個結構體來當作封閉空間，並將空間內的每個元素將會是特定scopeA下的識別字 和 特定scope B 的實體物件之間的對應關係，**在這裡的scope A和scope B 可能會是不一樣的或者不一樣**，而識別字可對應到scope B下的實體物件`
<!--SR:!2024-12-19,532,250-->

#🧠 在程式上，由兩個scope下內容而構成的closure是什麼樣的概念? 也請思考scope是否一樣？ ->->-> `具體會是一個結構體來當作封閉空間，並將空間內的每個元素將會是特定scopeA下的識別字 和 特定scope B 的實體物件之間的對應關係，**在這裡的scope A和scope B 可能會是不一樣的或者不一樣**，而識別字可對應到scope B下的實體物件`
<!--SR:!2024-06-16,311,229-->



#🧠 在程式上，closure會有什麼樣的用途？ ->->-> `以載入結構體的形式來允許程式碼能夠調用其他scope下的實體物件`
<!--SR:!2023-09-02,2,247-->


#🧠 若將該概念運用函式B能回傳函式A的情況下，且目前語言是支援first-class function，那麼closure具體是什麼樣的概念？ 以及如何保留closure所對應的實體物件是還在記憶體的？->->-> `函式A會因而成為函式物件，函式物件A的scope 會是上述的scope A，函式B的scope 會是上述的scope B，並且以scope A 為主來構築closure結構體或者集合，裡頭的元素會是多個scope A識別字和對應實體物件，這些scope A識別字部分對應著scope B的實體物件，部分對應著scope A的實體物件，且為了能讓**函式物件A繼續使用著函式B的實體物件，而允許即使函式B的EC要被釋放掉的情況下，還是會在具體實現上盡可能保留著函式A還會用到的函式B的實體物件**`
<!--SR:!2023-09-22,194,230-->


#🧠 若closure概念運用在支援first class function的語言，會是怎麼樣的運用 ->->-> `運用函式B能回傳函式A的情況下，並讓函式物件A擁有closure來透過識別字與其他scope下的實體物件做連接`
<!--SR:!2024-12-13,529,250-->


#🧠 以JS為例，來說明 garbage collector 主要是做什麼？->->-> `garbage collector 由於會觀察每個記憶體區塊被使用的情況來釋放，若確定記憶體區塊後續未被使用就會釋放；反之，若確定記憶體區塊後續還會被使用就會繼續保留。`
<!--SR:!2024-09-24,489,250-->

#🧠 以JS為例， garbage collector 如何判定哪些記憶體區塊是還在使用？並根據使用情況釋放？ ->->-> `- 編譯時來查看是否後續會被使用- 執行時根據演算法來確定，根據判定結果來判定未來後續是否被使用，沒被使用就被釋放，有被使用就保留`
<!--SR:!2024-11-17,514,250-->

#🧠 在沒有gc等記憶體保留政策下，請說明以下closure關係中的a在呼叫foo()時和之後的情況 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658674564/blog/javascript/closure/closure-garbage-collector-example_aszlox.png) ->->-> `當透過baz 來接收foo()所回傳的函式物件時，並且以該函式物件來呼叫時，而函式物件本身使用著foo下的a所對應的實體物件，理論上只要呼叫完foo，foo內的記憶體區塊將會被釋放，換言之，a也會被釋放，所以baz所印出的a會報錯`
<!--SR:!2024-11-16,513,250-->


#🧠 在有gc等記憶體保留政策下，請說明以下closure關係中的a在呼叫foo()時和之後的情況 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658674564/blog/javascript/closure/closure-garbage-collector-example_aszlox.png) ->->-> `因為函式宣告肯定會從編譯時期就分配記憶體以及查看每個識別字對應的實體物件是否後續有被使用，在這裏可以由於可從編譯時期確定後續會呼叫bar()，而bar會使用著foo下的a對應的對應實體物件，所以garbage collector確定後續會使用，所以不會釋放掉foo下的a對應的實體物件，**但就是沒釋放掉a對應的實體物件**，因而讓呼叫baz()時還能印出foo下的a的實體物件`
<!--SR:!2023-10-11,268,249-->

#🧠 若將closure運用函式B能回傳函式A的情況下，能做什麼樣用途？ ->->-> `讓函式物件擁有屬於自己的變數來存取和操作、打造成模組，並將function scope作為module scope來讓function回傳的function擁有module專有的變數`
<!--SR:!2025-01-09,541,250-->


#🧠 若要將closure運用函式B能回傳函式A的情況下，程式語言要具備什麼樣的特性才行？若要將closure運用函式B能回傳函式A的情況下，程式語言要具備什麼樣的特性才行？ ->->-> `必須要能夠把函式當作物件/值來看待的程式語言，即為支援first-class function的程式語言`
<!--SR:!2024-04-09,375,250-->


#🧠 若要運用函式B能回傳函式A的情況下，並且以JS來說明的話，每個closure如何獲取？如何對應？如何保留對應內容(Garbage Collector)？ ->->-> `- 每個函式物件A會具備closure結構體，其結構體會儲存每個函式物件A所用到的識別字以及對應的實體物件，該實體物件會是在函式物件A存在的實體物件或者函式B所存在的實體物件 - 若closure中的識別字對應著包含著函式物件A的函式B所擁有的實體物件時，會為了讓closure正常使用，而保留函式B的部分EC資訊，其資訊具會是函式物件A所用到的對應實體物件 - 至於函式B的EC資訊釋放則是看目前情況是否還滿足Garbage collector所依據的保留機制-若實體物件還繼續被參照使用的話，就會保留其記憶體，直到沒被使用，到時就會釋放 `
<!--SR:!2024-02-23,346,250-->



#🧠 請說明以下程式碼的執行是如何執行，有closure就說明為什麼？會報錯嗎？所使用的students和studentId會因此不見嗎？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658673001/blog/javascript/closure/closure-example_qknepx.png) ->->-> `- 每一個lookupStudent 函式會回傳一個greetStudent這函式物件， - 每個greetStudent由於是在被其他函式包含，所以會在編譯期間建立closure，來替每個識別字找到對應實體，除了students 和 studentId 這兩個識別字並不是greetStudent有的識別字，所以會根據scope chain往上尋找對應著包含greetStudent的函式所擁有的students 和 studentID - 而students 和 studentID並不會因為每次lookupStudent呼叫完畢才被釋放，而是因為能夠在編譯期間判定呼叫完畢後還會被使用，因此即使lookupStudent呼叫完畢，也會在使用的人還未結束執行會保留students 和 studentID`
<!--SR:!2023-10-31,104,229-->






---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[Execution Context 中的outer reference 適用以實現scope chain]]
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
[[first-class citizen 為一種實體，可以在特定程式語言下被當作是物件或值來看待，並且可以用物件和值所支援的操作來將實體和其他物件或值進行處理]]
References:
[[@simpsonYouDonKnow2022]]
[[@BiBaoJiSuanJiKeXue2022]]