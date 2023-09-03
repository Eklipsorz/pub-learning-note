## 描述

[[@naihuJavaScriptBianYiJIT]]
[[@linclarkCrashCourseJustintime]]

### JIT 引入至 JavaScript

> ## JIT

> JavaScript 刚出现的时候，是一个典型的解释型语言，因此运行速度极慢，后来浏览器引入了 **JIT compiler**，大幅提高了 JavaScript 的运行速度。

> 原理：They added a new part to the JavaScript engine, called a monitor (aka a profiler). That monitor watches the code as it runs, and **makes a note of how many times it is run and what types are used**.  

> 简单来说，浏览器在 JavaScript engine 中加入了一个 monitor，用来观察运行的代码。并记录下每段代码运行的次数和代码中的变量的类型。

> 那么问题来了，为什么这样做能提高运行速度？  
> 后面的所有内容都以下面这个函数的运行为例

```js
function arraySum(arr) {
  var sum = 0;
  for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
}
```

重點：
- JavaScript 在JIT之前，是將原始碼編譯成中間碼，並存於記憶體或者緩存，接著再邊轉中間碼為機械碼邊執行
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
- JIT 來臨時，JavaScript 會依據每個程式碼的執行頻率來進一步將執行頻率較高的程式碼編譯成更為效率的程式碼，主要會使用monitor，其monitor會負責：
	- 觀察正在執行的程式碼，並將為每段程式碼的**行數**和**原始碼轉換成bytecode並執行時所獲取的變數型別**作為索引，並以此計算程式碼的執行次數
- 執行次數超過x1，就會將對應索引的代碼設定為warm；如果執行次數超過x1且又超過x2，就會將對應索引的代碼設定hot，來分別使用頻率低和高。
- 依據monitor所得到的次數，會將次數高的程式碼試著再下一次執行前優化成更為效率的機械碼，具體會由：
	- Baseline Compiler：依據索引值來給定對應每次解析得到的機械碼，下次執行時直接從這取出機械碼執行，不用再解析
	- Optimizing Compiler：依據索引值來給定對應每次解析得到的機械碼，下次執行時直接從這取出機械碼執行，不用再解析，但這裡的機械碼會比Baseline Compiler來得有效率

### Interpreter 

> ## 1st step - Interpreter

> 一开始只是简单的使用解释器执行，当某一行代码被执行了几次，这行代码会被打上 **Warm** 的标签；当某一行代码被执行了很多次，这行代码会被打上 **Hot** 的标签

![](https://pic2.zhimg.com/80/v2-235cefb3de1873276264e6597d3d0819_720w.jpg)


重點：當JavaScript被編譯成ByteCode時，此時是剛執行的階段，
- 由於每段程式碼都是剛執行，所以一開始都會按照解釋器邊將BytecCode 轉換成機械碼 邊執行
- 每段程式碼都會在執行時都根據行數、原始碼資料類型來當索引在monitor那邊更新對應的執行次數：
	- 如果索引在monitor是不存在的話，就建立索引以及對應的執行次數為1
	- 如果索引在monitor是存在的話，就以對應索引來增加對應執行次數，如count = count + 1

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658511913/blog/javascript/compile/JIT/first-count-example_mbzuwv.png)

### Baseline Compiler

> ## 2nd step - Baseline compiler

> 被打上 **Warm** 标签的代码会被传给 **Baseline Compiler** 编译且储存，同时按照**行数 (Line number)** 和**变量类型 (Variable type)** 被索引（为什么会引入变量类型做索引很重要，后面会讲）

> 当发现执行的代码命中索引，会直接取出编译后的代码执行，从而不需要重复编译已经编译过的代码


![](https://pic1.zhimg.com/80/v2-de48ac228fa2e580ee301097df649dfc_720w.jpg)

重點：使用次數超過x1就為warm，使用次數超過x1且超過x2就為hot
- 使用次數次數超過x1但並不超過x2 的 索引所對應的程式碼會放在Baseline Compiler 並編譯成機械碼，並將機械碼放對應索引的機械碼欄位
- 下一次執行時，若發現命中同樣的索引，就以該對應的機械碼執行，而不需要重新編譯

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658511913/blog/javascript/compile/JIT/baseline-compiler-example_ofixlw.png)


### Optimizing compiler

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


重點：使用次數超過x1就為warm，使用次數超過x1且超過x2就為hot
- Optimizing compiler 採用的是 **假設特定行數和常出現的型別為主要前提，並為特定行數和型別所對應的bytecode編譯出更有效能的機械碼**，並依據假設成立概率來決定其機械碼的去留，若太低就會去除；若適當就會保留
- 使用次數超過x2的索引，並假設該索引的型別對應型別作為指定行數會是一直出現的型別，並且以索引內的行數作為 Optimizing compiler的索引，而前提就是目前索引內的型別，接著將對應的ByteCode和目前執行狀況來編譯成更為有效率的機械碼，至少比Baseline Compiler來得有效率，最後機械碼會是由行數來當索引，型別會是驗證是否繼續使用的標準 (line-> type, code)
- 當能在Optimizing compiler紀錄透過行數找到紀錄時，並目前索引下的型別與架設的型別一樣的話，就以索引對應的機械碼來執行；若型別不一樣的話，就以**baseline compiler能夠挑到的索引為主來挑對應機械碼** 或者 **無法在baseline compiler找到的話，則接著將對應bytecode丟進邊轉換machine code邊執行的元件**，並計數錯誤次數
- 當違反假設超過一定次數時，就捨棄目前索引對應的機械碼
- 效能部分：
	- 若假設成功率很高，效能會非常好
	- 若假設失敗率很低，效能會比沒有Optimizing compiler來得慢，因爲得經過優化，然後再轉為反優化的過程

这里就引申出两个问题，

1.  如何做合理的假设？
2.  假设失败率很高的时候怎么处理？

这里作者都有做解答，但是我觉得这不是重点我就直接把回答 copy 过来好了

> Answer 1: The optimizing compiler **uses the information the monitor has gathered by watching code execution to make these judgments**. If something has been true for all previous passes through a loop, it assumes it will continue to be true.  
>   
> Answer 2: Most browsers have **added limits to break out of these optimization/deoptimization cycles** when they happen. If the JIT has made more than, say, 10 attempts at optimizing and keeps having to throw it out, it will just stop trying

#### 檢查紀錄的優先權

1. 若optimizing compiler上有任何紀錄的話：
	每次執行時就去透過目前執行行數來在optimizing compiler紀錄上試著找到相對應的紀錄 -> 若找不到就看看目前執行行數和資料型別所構成的索引是否被標記warm -> 在沒有就去邊解析邊執行


2. 若optimizing compiler上沒有任何紀錄的話：
	每一次就透過目前行數和資料型別所構成的索引看是否標記warm -> 在沒有就去邊解析邊執行

### 整體流程

若使用次數沒超過x1就：
生成bytecode -> interepeter (邊編譯邊執行) -> 紀錄對應索引(line, type)的執行次數

若使用次數超過x1就且沒超過x2
- 未使用baseline compiler生成機械碼
生成bytecode -> 經過baseline compiler編譯成機械碼 -> 根據索引將機械碼紀錄至對應紀錄上的欄位 -> 以機械碼執行  ->  紀錄對應索引(line, type)的執行次數

- 已用baseline compiler 生成機械碼
生成bytecode ->  透過索引從monitor紀錄表格中找到對應機械碼 -> 以機械碼執行 ->  紀錄對應索引(line, type)的執行次數

若使用次數超過x2
- 未使用optimizing compiler生成機械碼
生成bytecode -> 經過optimizing compiler來根據目前執行狀態來編譯成更為有效執行的機械碼 ->將目前索引上的行數索引，並以型別作為是否能使用的假設標準 -> 以行數作為索引來儲存對應的機械碼：(line -> (type, code)) -> 以optimizing compiler對應的機械碼來執行->  紀錄對應索引(line, type)的執行次數

- 已用optimizing compiler 且假設成立
生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 -> 比較目前索引的型別是否與假設一樣 -> 若一樣的話，就以optimizing compiler對應的機械碼來執行 ->  紀錄對應索引(line, type)的執行次數

- 已用optmizing compiler 且假設錯誤
(若行數和對應的型別所構成的索引能夠在monitor找到對應紀錄且記錄為hot)
生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以baseline compiler的機械碼為主-> 紀錄錯誤次數 -> 紀錄對應索引(line, type)的執行次數

(若行數和對應的型別所構成的索引沒能在monitor標記warm或者沒在裡頭紀錄的話)
生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以對應的bytecode丟進邊將bytecode 轉成machine code邊執行的元件來執行 -> 紀錄錯誤 -> 紀錄對應索引(line, type)的執行次數

- 已用optmizing compiler 且錯誤次數達標

(若行數和對應的型別所構成的索引能夠在monitor找到對應紀錄且記錄為hot)
生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以baseline compiler的機械碼為主-> 紀錄錯誤次數 -> 刪除對應行數的optimizing compiler之機械碼紀錄 -> 紀錄對應索引(line, type)的執行次數


(若行數和對應的型別所構成的索引沒能在monitor標記warm或者沒在裡頭紀錄的話)
生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以對應的bytecode丟進邊將bytecode 轉成machine code邊執行的元件來執行-> 紀錄錯誤次數 -> 刪除對應行數的optimizing compiler之機械碼紀錄 -> 紀錄對應索引(line, type)的執行次數


## 複習
#🧠 JavaScript 在JIT之前，是如何編譯和執行(不用講得太仔細)->->-> `JavaScript 在JIT之前，是將原始碼編譯成中間碼，並存於記憶體或者緩存，接著再邊轉中間碼為機械碼邊執行`
<!--SR:!2023-09-09,27,250-->




#🧠 JavaScript 加入 JIT時，使用哪種辦法來應用JIT？->->-> `JavaScript 會依據每個程式碼的執行頻率來進一步將執行頻率較高的程式碼編譯成更為效率的程式碼`
<!--SR:!2023-09-10,28,250-->



#🧠 JavaScript 加入 JIT時，會使用什麼來觀察每個程式碼的執行頻率，具體怎麼計算？->->-> `monitor，觀察正在執行的程式碼，並將為每段程式碼的**行數**和**所用到的資料類型**作為索引，並以此計算程式碼的執行次數`
<!--SR:!2023-10-17,49,250-->


#🧠 JavaScript 的 JIT：如何區分哪些程式碼的執行頻率為稍高、高 ->->-> `當程式碼的執行次數高於x1時，就設定為代表稍高的warm，若執行次數高於x1且高於x2的話，就將對應的程式碼設為代表高的hot`
<!--SR:!2023-09-07,25,250-->


#🧠 JavaScript的JIT：當被標記為warm的程式碼，會如何做優化？ 誰負責優化->->-> `將對應的ByteCode放置Baseline Compiler，由它編譯成平時在interpreter編譯的機械碼版本並於monitor上的紀錄中找到對應索引，接著將機械碼放置對應索引的程式碼欄位，當下一次遇到同樣索引的ByteCode，就直接紀錄對應的機械碼取出並執行，不用重新編譯和執行`
<!--SR:!2023-09-06,24,250-->


#🧠 JavaScript的JIT：當被標記為hot的程式碼，會如何做優化？ 誰負責優化 ->->-> `將對應的bytecode放置optimizing compiler，由它以目前執行行數作為索引，並以目前處理的bytecode型別作為使用優化版本機械碼的憑證，接著將對應bytecode以及根據執行資訊編譯為更為有效率的機械碼版本並放置對應索引的機械碼，如(line)->(type, code)，當下一次執行同樣行數，就會檢查其型別是否和optimizing compiler一樣，若一樣就執行對應的機械碼`
<!--SR:!2023-09-05,23,250-->


#🧠 整體來說，在JIT版本的JavaScript中，monitor具體會以什麼做為資料上紀錄的索引->->-> `目前程式碼的行數和目前行數程式碼所擁有的型別`
<!--SR:!2023-09-09,27,250-->


#🧠 整體來說，在JIT版本的JavaScript中，monitor具體會以目前程式碼的行數和目前行數原始碼程式碼所擁有的型別做為資料上紀錄的索引，那麼型別會是指什麼？ ->->-> `原始碼轉換成bytecode並執行時所獲取的變數型別`
<!--SR:!2023-09-01,13,230-->



#🧠 整體來說，在JIT版本的JavaScript中，optimizing compiler具體會以什麼做為資料上紀錄的索引？ 以什麼標準作為可使用對應機械碼的許可->->-> `會以行數作為索引，並以設定的前提標準來當作標準，具體會是起初該行數被執行時的變數資料型別為標準，看每次同一行的資料型別是否和先前一樣，若一樣就核可。`
<!--SR:!2023-10-08,40,250-->


#🧠 JIT版本的JavaScript：以什麼標籤作為放進baseline compiler 的處理標準 ->->-> `擁有warm標籤的索引`
<!--SR:!2023-09-27,34,250-->


#🧠 JIT版本的JavaScript：以什麼標籤作為放進optiziming compiler 的處理標準 ->->-> `擁有hot標籤的索引`
<!--SR:!2023-10-02,38,250-->


#🧠 JIT版本的JavaScript：當JavaScript被編譯成ByteCode時，且此時為剛執行的階段，那麼JavaScript會如何執行ByteCode? 紀錄次數？ ->->-> `由於每段程式碼都是剛執行，所以一開始都會按照解釋器邊將BytecCode 轉換成機械碼 邊執行，每段程式碼都會在執行時都根據行數、資料類型來當索引在monitor那邊更新對應的執行次數`
<!--SR:!2023-09-09,27,250-->


#🧠 JIT版本的JavaScript：當JavaScript被編譯成ByteCode並執行時，會如何monitor計數執行次數？ ->->-> `如果索引在monitor是不存在的話，就建立索引以及對應的執行次數為1、如果索引在monitor是存在的話，就以對應索引來增加對應執行次數，如count = count + 1`
<!--SR:!2023-09-04,22,250-->



#🧠 JIT版本的JavaScript：試說明以下紀錄是如何產生的![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658511913/blog/javascript/compile/JIT/first-count-example_mbzuwv.png)->->-> `scope是指處於哪一個scope，如特定function或者global，line是指scope下的第幾行，type是該行數的程式碼是用哪些型別，count是對應程式碼被執行了多少次，在這裏是在arraySum函式下執行它的內容並從執行過程獲取出來的資料`
<!--SR:!2023-10-14,46,250-->

#🧠 JIT版本的JavaScript：假設超過x1且不超過x2就為warm，那麼假使某索引的程式碼的執行次數剛好符合，請問會如何執行對應程式碼？ 若下次相同索引會如何執行？ ->->-> ` 會將對應的bytecode編譯成機械碼並跟索引來將機械碼放置monitor紀錄上，接著直接以該機械碼執行，未來碰上相同的索引就會以monitor能夠對應到的機械碼來執行，不用重新編譯並且執行`
<!--SR:!2023-10-19,51,250-->


#🧠 JIT版本的JavaScript：假設目前optimizing compiler上沒任何紀錄，但monitor有紀錄且有warm，請問每一次程式碼的執行會如何進行？（考慮為warm和不為warm的情況下) ->->-> `每一次執行就會以目前執行行數和型別來構成索引來從monitor找到對應紀錄，看是否為warm，若warm的話，就取出對應的機械碼執行，若不是的話，就交給interpreter邊轉化機械碼邊執行`
<!--SR:!2023-10-24,54,250-->


#🧠 JIT版本的JavaScript：試說明被標記為warm的原始碼發生了什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658511913/blog/javascript/compile/JIT/baseline-compiler-example_ofixlw.png)->->-> `在這裡由於arraySum函式的由(行數, 型別)所構成的索引之執行次數達標，所以就將對應的bytecode放到baseline compiler編譯成機械碼，然後根據索引來將機械碼更新至monitor上的紀錄，就如同最右邊的code，下次碰上相同的索引就以monitor上的紀錄來找到對應的機械碼執行`
<!--SR:!2023-10-11,43,250-->


#🧠 JIT版本的JavaScript：假設超過x2就為hot，那麼假使某索引的程式碼的執行次數剛好符合，請問會如何執行對應程式碼？ 若下次相同索引(optimizing compiler)的話，會如何處理？ ->->-> `會以目前索引下的行數作為optimizing compiler的紀錄索引，並用目前索引下的型別作為前提或者假設，接著再將索引對應的bytecode和目前執行情況編譯成更為有效率的機械碼並依據行數來將機械碼放置optimizing compiler的對應紀錄上，最後以機械碼執行，下次當執行的程式碼行數是能夠在optimizing compiler紀錄能夠找到，就會比對其型別是否和前提一樣，若一樣從optimizing compiler取出對應行數的機械碼來執行`
<!--SR:!2023-09-08,26,250-->


#🧠 JIT版本的JavaScript：假設目前optimizing compiler上有任何紀錄，請問每一次程式碼的執行會如何進行？ ->->-> `每次執行就去會利用目前執行行數作為索引去在optimizing compiler找到相對應的紀錄，若找到對應行數，就會比對目前執行的程式碼所擁有的型別是否和紀錄上的假設一樣，若一樣就執行對應的機械碼，若不一樣的話，就要看看目前行數和目前型別是否能夠在baseline compiler找到對應紀錄，有的話，就以baseline compiler的機械碼為主，沒的話，就將對應bytecode丟進interpreter來邊轉換成機械碼邊執行`
<!--SR:!2023-09-10,28,250-->


#🧠 JIT版本的JavaScript： 若目前程式碼能夠依照行數從目前optimizing compiler到對應的假設和機械碼，但目前型別不符合假設，會如何？->->-> `會計算不符合的次數，並且轉換成baseline compiler版本的機械碼或者交由interpreter來邊編譯邊執行`
<!--SR:!2023-10-15,47,250-->


#🧠 JIT版本的JavaScript： 若目前程式碼能夠依照行數從目前optimizing compiler到對應的假設和機械碼，但目前型別不符合假設的次數達到某種程度時，會是？->->-> `當違反假設超過一定次數時，就捨棄目前索引對應的機械碼，並且轉換成baseline compiler版本的機械碼或者交由interpreter來邊編譯邊執行`
<!--SR:!2023-10-23,53,250-->



#🧠 JIT版本的JavaScript： 若optimizing compiler的假設成功率很高的話，會是什麼？為什麼呢？ ->->-> `代表著都一直執行非常有效率的機械碼，效能會非常好`
<!--SR:!2023-09-10,28,250-->


#🧠 JIT版本的JavaScript： 若optimizing compiler的假設成功率很低的話，會是什麼？ ->->-> `效能會比沒有Optimizing compiler來得慢，因爲得經過優化，然後再轉為反優化的過程`
<!--SR:!2023-09-10,12,230-->



#🧠 JIT版本的JavaScript：檢查紀錄的優先權，若optimizing compiler上有任何紀錄的話 ->->-> `每次執行時就去透過目前執行行數來在optimizing compiler紀錄上試著找到相對應的紀錄 -> 若找不到就看看目前執行行數和資料型別所構成的索引是否被標記warm -> 在沒有就去邊解析邊執行`
<!--SR:!2023-09-04,22,250-->


#🧠 JIT版本的JavaScript：檢查紀錄的優先權，若optimizing compiler上沒有任何紀錄的話->->-> `每一次就透過目前行數和資料型別所構成的索引看是否標記warm -> 在沒有就去邊解析邊執行`
<!--SR:!2023-10-30,57,250-->



#🧠 JIT版本的JavaScript：假設x1為warm的標準，若對應索引為使用次數沒超過x1的話，流程會是什麼？ ->->-> `生成bytecode -> interepeter (邊編譯邊執行) -> 紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-29,36,250-->

#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若使用次數超過x1就且沒超過x2，且未使用baseline compiler生成機械碼，流程會是什麼？->->-> `生成bytecode -> 經過baseline compiler編譯成機械碼 -> 根據索引將機械碼紀錄至對應紀錄上的欄位 -> 以機械碼執行  ->  紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-06,24,250-->


#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若使用次數超過x1就且沒超過x2，已用baseline compiler 生成機械碼，流程會是什麼？ ->->-> `生成bytecode ->  透過索引從monitor紀錄表格中找到對應機械碼 -> 以機械碼執行 ->  紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-06,24,250-->


#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，且未使用optimizing compiler生成機械碼，流程會是什麼？->->-> `生成bytecode -> 經過optimizing compiler來根據目前執行狀態來編譯成更為有效執行的機械碼 ->將目前索引上的行數索引，並以型別作為是否能使用的假設標準 -> 以行數作為索引來儲存對應的機械碼：(line -> (type, code)) -> 以optimizing compiler對應的機械碼來執行->  紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-08,26,250-->



#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，已用optimizing compiler 且假設成立，流程會是什麼？ ->->-> `生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 -> 比較目前索引的型別是否與假設一樣 -> 若一樣的話，就以optimizing compiler對應的機械碼來執行 ->  紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-05,23,250-->



#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，已用optmizing compiler 且假設錯誤，流程會是什麼？(若行數和對應的型別所構成的索引能夠在monitor找到對應紀錄且記錄為hot) ->->-> `(若行數和對應的型別所構成的索引能夠在monitor找到對應紀錄且記錄為hot) 生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以baseline compiler的機械碼為主-> 紀錄錯誤次數 -> 紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-10-01,37,250-->



#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，已用optmizing compiler 且假設錯誤，流程會是什麼？(若行數和對應的型別所構成的索引沒能在monitor標記warm或者沒在裡頭紀錄的話)  ->->-> `生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以對應的bytecode丟進邊將bytecode 轉成machine code邊執行的元件來執行 -> 紀錄錯誤 -> 紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-07,25,250-->



#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，已用optmizing compiler 且錯誤次數達標，流程會是什麼？(若行數和對應的型別所構成的索引能夠在monitor找到對應紀錄且記錄為hot)  ->->-> `生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以baseline compiler的機械碼為主-> 紀錄錯誤次數 -> 刪除對應行數的optimizing compiler之機械碼紀錄 -> 紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-08,26,250-->


#🧠 JIT版本的JavaScript：假設x1為warm的標準，x2為hot的標準，若索引的使用次數超過x2，已用optmizing compiler 且錯誤次數達標，流程會是什麼？(若行數和對應的型別所構成的索引沒能在monitor標記warm或者沒在裡頭紀錄的話) ->->-> `生成bytecode -> 透過目前索引的行數試著能夠在optimizing compiler中找到對應的機械碼 ->  比較目前索引的型別是否與假設一樣 -> 若不一樣的話，就以對應的bytecode丟進邊將bytecode 轉成machine code邊執行的元件來執行-> 紀錄錯誤次數 -> 刪除對應行數的optimizing compiler之機械碼紀錄 -> 紀錄對應索引(line, type)的執行次數`
<!--SR:!2023-09-07,25,250-->



---
Status: #🌱
Tags:
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
References:
[[@naihuJavaScriptBianYiJIT]]
[[@linclarkCrashCourseJustintime]]
[[@JSYinQingYiJSZhongDeJITYuJiBenZhiXingLuoJi]]