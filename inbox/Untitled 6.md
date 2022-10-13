## 描述

[[@mdnClassesJavaScriptMDN]]
> The static keyword defines a static method or property for a class. Static members (properties and methods) are called without instantiating their class and cannot be called through a class instance. Static methods are often used to create utility functions for an application, whereas static properties are useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances. 


[[@mdnStaticMethodMDN]]
> A static method (or static function) is a method defined as a member of an object but is accessible directly from an API object's constructor, rather than from an object instance created via the constructor.

> In a Web API, a static method is one which is defined by an interface but can be called without instantiating an object of that type first.
>
> Methods called on object instances are called instance methods. 


[[@khanacademyStaticFunctionsVs]]
> A "static" function is a function that is defined on an object, but it doesn't change properties of the object. So why even define it on the object? Typically, it has something to do with the object, so it is logical to attach it to it. It treats the object more like a namespace.





### static variable 命名緣由
[[@wikidataStaticVariable2022]]
> In computer programming, a static variable is a variable that has been allocated "statically", meaning that its lifetime (or "extent") is the entire run of the program


重點：
- static variable 中 的static 起源於static memory allocation作法
- static variable 意旨為在執行前就已經分配好記憶體



#### static memory allocation vs. dynamic memory allocation
[[@geeksforgeeksDifferenceStaticDynamic2020]]
> **Static Memory Allocation:** Static Memory is allocated for declared variables by the compiler.

> **Dynamic Memory Allocation:** Memory allocation done at the time of execution(run time) is known as **dynamic memory allocation**



重點：
- static memory allocation：相對於dynamic memory allocation來說，會以不透過執行程式來進行記憶體分配，換言之，就是在執行階段前做記憶體分配
- dynamic memory allocation：相對於static memory allocation來說，會以透過執行程式來根據執行狀態作為記憶體分配的依據，換言之，就是在執行階段做記憶體分配




### static 命名緣由

> staying in one place without moving, or not changing for a long time




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@mdnClassesJavaScriptMDN]]
[[@khanacademyStaticFunctionsVs]]
[[@mdnStaticMethodMDN]]
[[@geeksforgeeksDifferenceStaticDynamic2020]]
[[@wikidataStaticVariable2022]]