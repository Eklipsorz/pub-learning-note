



## 描述

> Closure is a behavior of functions and only functions. If you aren't dealing with a function, closure does not apply. An object cannot have closure, nor does a class have closure (though its functions/methods might). Only functions have closure.

重點：
- 除了函式以外，就只有function能夠構築closure


在程式上，是一種多個scope層級之間的對應關係上的封閉空間，換言之，封閉空間內的每個元素將會是特定scopeA下的識別字 和 特定scope B 的實體物件之間的對應關係，在這裡的scope A和scope B會是不一樣的，而識別字可對應到scope B下的實體物件。

- 
   
   會將識別字和對應物件綁定在一塊構成一個結構體，在這裡會是以Execution Context來表示。
	- 嚴謹來說，一個EC

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

Each of those references from the inner function to the variable in an outer scope is called a _closure_. In academic terms, each instance of `greetStudent(..)` _closes over_ the outer variables `students` and `studentID`.



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


Closure 從數學引申過來成封閉的空間，也就是將函式與一組資料變數綁定在一個封閉空間，以至於只有該函式能夠修改該資料變數




![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658653407/blog/javascript/closure/You_Don_t_Know_JS_Yet-Closure1_wbgcko.jpg)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658653407/blog/javascript/closure/You_Don_t_Know_JS_Yet-Closure2_xo614o.jpg)


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