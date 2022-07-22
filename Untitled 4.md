## 描述

[[@naihuJavaScriptBianYiJIT]]
[[@linclarkCrashCourseJustintime]]
> ## JIT

> JavaScript 刚出现的时候，是一个典型的解释型语言，因此运行速度极慢，后来浏览器引入了 **JIT compiler**，大幅提高了 JavaScript 的运行速度。

> 原理：They added a new part to the JavaScript engine, called a monitor (aka a profiler). That monitor watches the code as it runs, and **makes a note of how many times it is run and what types are used**.  

> 简单来说，浏览器在 JavaScript engine 中加入了一个 monitor，用来观察运行的代码。并记录下每段代码运行的次数和代码中的变量的类型。

> 那么问题来了，为什么这样做能提高运行速度？  
后面的所有内容都以下面这个函数的运行为例

```js
function arraySum(arr) {
  var sum = 0;
  for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
}
```

> ## 1st step - Interpreter

> 一开始只是简单的使用解释器执行，当某一行代码被执行了几次，这行代码会被打上 **Warm** 的标签；当某一行代码被执行了很多次，这行代码会被打上 **Hot** 的标签

![](https://pic2.zhimg.com/80/v2-235cefb3de1873276264e6597d3d0819_720w.jpg)


> ## 2nd step - Baseline compiler

> 被打上 **Warm** 标签的代码会被传给 **Baseline Compiler** 编译且储存，同时按照**行数 (Line number)** 和**变量类型 (Variable type)** 被索引（为什么会引入变量类型做索引很重要，后面会讲）

> 当发现执行的代码命中索引，会直接取出编译后的代码执行，从而不需要重复编译已经编译过的代码


![](https://pic1.zhimg.com/80/v2-de48ac228fa2e580ee301097df649dfc_720w.jpg)

> ## 3rd step - Optimizing compiler

> 被打上 **Hot** 标签的代码会被传给 **Optimizing compiler**，这里会对这部分带码做更优化的编译。怎么样做更优化的编译呢？关键点就在这里，没有别的办法，只能用概率模型做一些合理的 **”假设 (Assumptions)“**。

![](https://pic1.zhimg.com/80/v2-ee45b1a7a7c68f1a4ba46c5a376ba18c_720w.jpg)

> 比如我们上面的循环中的代码 `sum += arr[i]`，尽管这里只是简单的 `+` 运算和赋值，但是因为 JavaScript 的**动态类型 (Dynamic typing)**，对应的编译结果有很多种可能（这个角度能很明显的暴露动态类型的缺点）

> 比如

> -   sum 是 Int，arr 是 Array，i 是 Int，这里的 `+` 就是加法运算，对应其中一种编译结果
> -   sum 是 string，arr 是 Array，i 是 Int，这里的 `+` 就是字符串拼接，并且需要把 i 转换为 string 类型
> -   ...

> 下面的图可以看出，这么简单的一行代码对应有 2^4 = 16 种可能的编译结果


![](https://pic1.zhimg.com/80/v2-b59e89cbf144adcc2b938db84a4fc9d8_720w.jpg)

> 前面第二步的 Baseline compiler 做的就是这件事，所以上面说编译后的代码需要使用 **line number** 和 **variable type** 一起做索引，因为不同的 variable type 对应不同的编译结果。

> 如果代码是 **"Warm"** 的，JIT 的任务也就到此为止，后面每次执行的时候，需要先判断类型，再使用对应类型的编译结果就好。

![](https://pic4.zhimg.com/80/v2-04b4d6fb3b1e55b30f04a208d206e74f_720w.jpg)


> 但是上面我们说，当代码变成 **"hot"** 的时候，会做更多的优化。这里的优化其实指的就是 JIT 直接假设一个前提，比如这里我们直接假设 sum 是 Int，i 也是 Int，arr 是 Array，于是就只用一种编译结果就好了。


![](https://pic2.zhimg.com/80/v2-37d5258e27e301f78c3c5a3e439e4edd_720w.jpg)


> 实际上，在执行前会做类型检查，看是假设是否成立，如果不成立执行就会被打回 interpreter 或者 baseline compiler 的版本，这个操作叫做 "反优化 (deoptimization)"。

> 可以看出，只要假设的成功率足够高，那么代码的执行速度就会快。但是如果假设的成功率很低，那么会导致比没有任何优化的时候还要慢（因为要经历 optimize => deoptimize 的过程）

![](https://pic3.zhimg.com/80/v2-3d59f5542434ae6d07e4223fb7e32fce_720w.jpg)

这里就引申出两个问题，

1.  如何做合理的假设？
2.  假设失败率很高的时候怎么处理？

这里作者都有做解答，但是我觉得这不是重点我就直接把回答 copy 过来好了

> Answer 1: The optimizing compiler **uses the information the monitor has gathered by watching code execution to make these judgments**. If something has been true for all previous passes through a loop, it assumes it will continue to be true.  
>   
> Answer 2: Most browsers have **added limits to break out of these optimization/deoptimization cycles** when they happen. If the JIT has made more than, say, 10 attempts at optimizing and keeps having to throw it out, it will just stop trying

## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:

[[@naihuJavaScriptBianYiJIT]]
[[@linclarkCrashCourseJustintime]]
[[@JSYinQingYiJSZhongDeJITYuJiBenZhiXingLuoJi]]