



## 描述

> Closure is a behavior of functions and only functions. If you aren't dealing with a function, closure does not apply. An object cannot have closure, nor does a class have closure (though its functions/methods might). Only functions have closure.

重點：
- 除了函式以外，就只有function能夠構築closure

### closure 在電腦語言下的意思
> 是在支援頭等函式的程式語言中實現詞法繫結的一種技術。閉包在實現上是一個結構體，它儲存了一個函式（通常是其入口位址）和一個關聯的環境（相當於一個符號尋找表）。環境裡是若干對符號和值的對應關係，它既要包括約束變數（該函式內部繫結的符號），也要包括自由變數（在函式外部定義但在函式內被參照），有些函式也可能沒有自由變數。閉包跟函式最大的不同在於，當捕捉閉包的時候，它的自由變數會在捕捉時被確定，這樣即便脫離了捕捉時的上下文，它也能照常執行。捕捉時對於值的處理可以是值拷貝，也可以是名稱參照，這通常由語言設計者決定，也可能由使用者自行指定（如C++）。

1. 在程式上，是一種多個scope層級之間的對應關係上的封閉空間
2. 換言之，封閉空間內的每個元素將會是特定scopeA下的識別字 和 特定scope B 的實體物件之間的對應關係，**在這裡的scope A和scope B 可能會是不一樣的**，而識別字可對應到scope B下的實體物件
3. 具體用途為：
	- 以載入結構體的形式來允許程式碼能夠調用其他scope下的實體物件
4.  該概念會運用在函式A和包含函式A的函式B上，函式A的scope 會是上述的scope A，函式B的scope 會是上述的scope B，並且以scope A 為主來構築closure結構體或者集合，裡頭的元素會是多個scope A識別字和對應實體物件，這些scope A識別字部分對應著scope B的實體物件，部分對應著scope A的實體物件，且為了能讓**函式A繼續使用著函式B的實體物件，而允許即使函式B的EC要被釋放掉的情況下，還是會在具體實現上盡可能保留著函式A還會用到的函式B的實體物件**
> A closure is a function having access to the parent scope, even after the parent function has closed.

總結來說的話：
- 每個函式A會具備closure結構體，其結構體會儲存每個函式A所用到的識別字以及對應的實體物件，該實體物件會是在函式A存在的實體物件或者是包含函式A的函式B所存在的實體物件
- 若closure中的識別字對應著包含著函式A的函式B所擁有的實體物件時，會為了讓closure正常使用，而保留函式B的部分EC資訊，其資訊具會是函式A所用到的對應實體物件
- 至於函式B的EC資訊釋放則是看目前情況是否還滿足Garbage collector所依據的保留機制-若實體物件還繼續被參照使用的話，就會保留其記憶體，直到沒被使用，到時就會釋放


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

> For closure to be observed, a function must be invoked, and specifically it must be invoked in a different branch of the scope chain from where it was originally defined. A function executing in the same scope it was defined would not exhibit any observably different behavior with or without closure being possible; by the observational perspective and definition, that is not closure.
> 
> Let's look at some code, annotated with its relevant scope bubble colors (see Chapter 2):


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


> The first thing to notice about this code is that the `lookupStudent(..)` outer function creates and returns an inner function called `greetStudent(..)`. `lookupStudent(..)` is called twice, producing two separate instances of its inner `greetStudent(..)` function, both of which are saved into the `chosenStudents` array.

> We verify that's the case by checking the `.name` property of the returned function saved in `chosenStudents[0]`, and it's indeed an instance of the inner `greetStudent(..)`.

> After each call to `lookupStudent(..)` finishes, it would seem like all its inner variables would be discarded and GC'd (garbage collected). The inner function is the only thing that seems to be returned and preserved. But here's where the behavior differs in ways we can start to observe.

> While `greetStudent(..)` does receive a single argument as the parameter named `greeting`, it also makes reference to both `students` and `studentID`, identifiers which come from the enclosing scope of `lookupStudent(..)`. Each of those references from the inner function to the variable in an outer scope is called a _closure_. In academic terms, each instance of `greetStudent(..)` _closes over_ the outer variables `students` and `studentID`.


### 從觀察獲取closure 


> Each of those references from the inner function to the variable in an outer scope is called a _closure_. In academic terms, each instance of `greetStudent(..)` _closes over_ the outer variables `students` and `studentID`.

JavaScript


> So what do those closures do here, in a concrete, observable sense?

> Closure allows `greetStudent(..)` to continue to access those outer variables even after the outer scope is finished (when each call to `lookupStudent(..)` completes). Instead of the instances of `students` and `studentID` being GC'd, they stay around in memory. At a later time when either instance of the `greetStudent(..)` function is invoked, those variables are still there, holding their current values.

> If JS functions did not have closure, the completion of each `lookupStudent(..)` call would immediately tear down its scope and GC the `students` and `studentID` variables. When we later called one of the `greetStudent(..)` functions, what would then happen?

> If `greetStudent(..)` tried to access what it thought was a BLUE(2) marble, but that marble did not actually exist (anymore), the reasonable assumption is we should get a `ReferenceError`, right?

> But we don't get an error. The fact that the execution of `chosenStudents[0]("Hello")` works and returns us the message "Hello, Sarah!", means it was still able to access the `students` and `studentID` variables. This is a direct observation of closure!

### Pointed Closure

> Actually, we glossed over a little detail in the previous discussion which I'm guessing many readers missed!

> Because of how terse the syntax for `=>` arrow functions is, it's easy to forget that they still create a scope (as asserted in "Arrow Functions" in Chapter 3). The `student => student.id == studentID` arrow function is creating another scope bubble inside the `greetStudent(..)` function scope.

> Building on the metaphor of colored buckets and bubbles from Chapter 2, if we were creating a colored diagram for this code, there's a fourth scope at this innermost nesting level, so we'd need a fourth color; perhaps we'd pick ORANGE(4) for that scope:


```

var student = students.find(
    student =>
        // function scope: ORANGE(4)
        student.id == studentID
);
```


> The BLUE(2) `studentID` reference is actually inside the ORANGE(4) scope rather than the GREEN(3) scope of `greetStudent(..)`; also, the `student` parameter of the arrow function is ORANGE(4), shadowing the GREEN(3) `student`.

> The consequence here is that this arrow function passed as a callback to the array's `find(..)` method has to hold the closure over `studentID`, rather than `greetStudent(..)` holding that closure. That's not too big of a deal, as everything still works as expected. It's just important not to skip over the fact that even tiny arrow functions can get in on the closure party.





### Closure 命名緣由
[[@simpsonYouDonKnow2022]] 所描述：
>  Closure is originally a mathematical concept, from lambda calculus. But I'm not going to list out math formulas or use a bunch of notation and jargon to define it.

1. 從數學概念-Closure衍伸過來的術語，意為著包含著特定物件的封閉空間


閉包可以用來在一個函式與一組「私有」變數之間建立關聯關係
https://zh.m.wikipedia.org/zh-tw/闭包_(计算机科学)



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[Execution Context 中的outer reference 適用以實現scope chain]]
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
References:
[[@simpsonYouDonKnow2022]]