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


重點：
- 在JS中，class 內部定義static method 或者 static property，代表著已經在執行前分配好記憶體給method或者property，換言之，就是不透過執行物件的實例化過程來分配，而是單方面在執行之前分配好記憶題的變數或者函式
- static method 用途：
	- 作為utility function來使用，而class名稱就表明該function的隸屬
- static property 用途：
	- 作為特定設定資料的緩存，而class名稱就表明這份資料的隸屬
- 細節：
	- 由於static method 和 static property 本身就不透過執行實例化來分配記憶體，所以即使重複執行多次 new function() 也不會替static method / property製作成副本


### static variable 命名緣由
[[@wikidataStaticVariable2022]]
> In computer programming, a static variable is a variable that has been allocated "statically"


重點：
- static variable 中 的static 起源於static memory allocation作法
- static variable 意旨為在執行前就已經分配好記憶體給變數
- static function / static method 意旨為在執行前就已經分配好記憶體給函式



#### static memory allocation vs. dynamic memory allocation
[[@geeksforgeeksDifferenceStaticDynamic2020]]
> **Static Memory Allocation:** Static Memory is allocated for declared variables by the compiler.

> **Dynamic Memory Allocation:** Memory allocation done at the time of execution(run time) is known as **dynamic memory allocation**



重點：
- static memory allocation：相對於dynamic memory allocation來說，會以不透過執行程式來進行記憶體分配，換言之，就是在執行階段前做記憶體分配
- dynamic memory allocation：相對於static memory allocation來說，會以透過執行程式來根據執行狀態作為記憶體分配的依據，換言之，就是在執行階段做記憶體分配




### static 命名緣由

> staying in one place without moving, or not changing for a long time

> Something that is static does not move or change.

重點：
- 若某事物是static 的話，那麼就是指某事物並不會移動或者並不會改變

## 複習


#🧠  static 命名緣由->->-> `若某事物是static 的話，那麼就是指某事物並不會移動或者並不會改變`
<!--SR:!2024-10-09,443,250-->

#🧠 static memory allocation 是什麼？(簡述) ->->-> `相對於dynamic memory allocation來說，會以不透過執行程式來進行記憶體分配，換言之，就是在執行階段前做記憶體分配，而是單方面在執行之前分配好記憶題的變數或者函式`
<!--SR:!2023-11-10,141,210-->


#🧠  static memory allocation 為什麼會有static來稱呼?  ->->-> `相對於dynamic memory allocation來說`
<!--SR:!2024-02-10,221,246-->

#🧠  dynamic memory allocation 為什麼會有dynamic來稱呼?  ->->-> `相對於static memory allocation來說`
<!--SR:!2024-03-19,251,246-->


#🧠 dynamic memory allocation 是什麼？(簡述) ->->-> `相對於static memory allocation來說，會以透過執行程式來根據執行狀態作為記憶體分配的依據，換言之，就是在執行階段做記憶體分配，而是單方面在執行之前分配好記憶題的變數或者函式`
<!--SR:!2025-01-13,508,250-->


#🧠 在JS中的class內部定義static method或者static property，其記憶體狀況為何？ ->->-> `代表著已經在執行前分配好記憶體給method或者property，換言之，就是不透過執行物件的實例化過程來分配`
<!--SR:!2023-12-31,166,246-->


#🧠 在JS中的static method的用途為何？class對於static method的描述會是什麼？ ->->-> `作為utility function來使用，而class名稱就表明該function的隸屬`
<!--SR:!2023-12-09,102,230-->

#🧠 在JS中的static property的用途為何？class對於static property的描述會是什麼？->->-> `作為特定設定資料的緩存，而class名稱就表明這份資料的隸屬`
<!--SR:!2024-03-26,252,230-->

#🧠  static variable 中 的static 起源於什麼？ ->->-> `static variable 中 的static 起源於static memory allocation作法`
<!--SR:!2025-01-12,507,250-->

#🧠 static variable 是什麼？->->-> `static variable 意旨為在執行前就已經分配好記憶體給變數`
<!--SR:!2025-01-18,512,250-->

#🧠 static function / static method是什麼？ ->->-> `static function / static method 意旨為在執行前就已經分配好記憶體給函式`
<!--SR:!2023-12-11,104,230-->

#🧠 static variable 對於JS的class來說是什麼樣的記憶體區塊？->->-> `就是不透過執行物件的實例化過程來分配，而是單方面在執行之前分配好記憶體的變數或者函式`
<!--SR:!2024-07-10,358,230-->




#🧠 請問若JS class的實例化執行好N次，請問class 下的每個static method會有幾份副本？為什麼？->->-> `都各1份，因為就以單方面在執行之前分配好記憶題的變數或者函式，所以即使重複執行多次 new function() 也不會替static method / property製作成副本`
<!--SR:!2024-09-15,425,250-->

#🧠 請問若JS class的實例化執行好N次，請問class 下的static property會有幾份副本？為什麼？->->-> `都各1份，因為就以單方面在執行之前分配好記憶題的變數或者函式，所以即使重複執行多次 new function() 也不會替static method / property製作成副本`
<!--SR:!2024-09-13,423,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnClassesJavaScriptMDN]]
[[@khanacademyStaticFunctionsVs]]
[[@mdnStaticMethodMDN]]
[[@geeksforgeeksDifferenceStaticDynamic2020]]
[[@wikidataStaticVariable2022]]