## 描述


### 模組載入方式分為三階段

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段(在這裡CommonJS並不會特意分割這三個階段)



### CommonJS源自於伺服器端

CommonJS 本身是源自於伺服器端的模組化標準，由於那時其模組皆源自於伺服器本機端，只考量如從硬碟獲取對應模組內容並載入至特定區塊，所以並沒有考量網路上的傳輸延遲問題，網路上的傳輸延遲會比從本機端獲取模組來得慢。

### 是否擁有模組依賴關係圖

是，主要用來遍歷模組來找到需要處理的模組以及檢測是否發生環狀依賴關係結構


### 單個CommonJS模組的載入
> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.

![](https://hacks.mozilla.org/files/2018/03/13_static_import-768x225.png)


當需求方以Require來指定特定JS檔案，就會將JS檔案視為CommonJS模組檔案，這時JS引擎會先於編譯期間做：
- 分配記憶體空間給模組下的模組實例module物件、var變數宣告、函式宣告
- 分配初始值給var變數為undefined、函式宣告會是拿到存放函式內容的記憶體區塊、模組實例(exports部分會是{} )
- 建立EC來紀錄模組下的每個識別字和對應實體物件

接著執行該模組的top-level code 來產生模組要輸出的內容以及執行輸出模組內容的語句，如：執行到下列語句才會把輸出內容從空物件轉換成指定內容

```
exports = module.exports = ....
```



> This is different from CommonJS modules. In CommonJS, the entire export object is copied on export. This means that any values (like numbers) that are exported are copies.

> This means that if the exporting module changes that value later, the importing module doesn’t see that change.

編譯時期就會分配記憶體來存放模組所要輸出的內容，而執行下列語句只是確定輸出內容為何。
```
exports = module.exports = ....
```
![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)

而執行require的那一方會從實際上會將存放在記憶體的模組實例複製一份讓執行require的那一方獲取副本，所以實際上是透過執行該模組來產生對應模組實例，然後讓require的那一方獲取模組實例的副本。
```
const xxx = require(module1)
```
### CommonJS 特點

CommonJS設計上會是：

1.  以單執行緒來去加載模組 
2. 以模組在本機端儲存設備上為前提而設計
3. 同步加載：目前模組的載入必須等待前面模組的載入階段都完成才能做
4.  載入形式：透過執行模組來載入模組實例至需求方
5.  沒特意將模組載入細分成獲取&建構、實例化、確定值這幾個階段，主要會用DFS Post-Order Traversal 來遍歷模組依賴關係圖來找到需要處理的模組，並且將找到的模組一次性處理獲取&建構、實例化


### DFS遍歷模組依賴關係例子
依賴模組：
1. main 模組依賴著M1模組、M2模組、M3模組
2. M1 模組依賴M4 模組、M5模組
3. M2 模組依賴M6模組


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659287023/blog/javascript/module/commonjs-module-example_vovrps.png)


首先一開始從main.js執行，並且為了載入module1而執行對應Module1模組來獲取對應模組輸出內容，接著module1模組在一開始表明依賴著module4，所以就轉而去執行module4來獲取其模組輸出內容，由於Module4模組沒再依賴任何模組，所以就直接印出this is module4並輸出指定
內容給module1當module4所參照的物件，接著執行權就從M4回轉至M1，並由M1來執行module5來獲取對應輸出內容，而module5並沒有任何依賴模組的需求就直接印出this is module5 並輸出指定內容給M1，接著執行權回到M1，M1已經載入完成，就印出this is module1，接著就輸出自己模組的內容至main模組所要參照的模組物件。

執行權回到main.js，並轉由執行module2來獲取其模組輸出內容，而module2依賴著Module6，因而執行module6來獲取其模組輸出內容，module6並沒有依賴模組，所以就執行印出this is module6，然後就輸出模組內容至module2當參照物件，接著執行權回到M2，M2也載入所有依賴模組，就直接印出this is module2，接著輸出自己模組內容至main.js當參照內容，執行權回到main.js，而main.js此時只剩module3還未載入，就執行Module3來獲取對應模組內容，module3本身沒有依賴模組，所以只需要執行印出this is module3，然後輸出自己模組內容至main.js當參照物件，最後執行權回到main.js，main.js也載入所有依賴模組，這時就會執行main.js的內容，也就是this is main。

所以順序會是：this is module 4 -> this is module 5 -> this is module 1 -> this is module 6 -> this is module 2 -> this is module 3 -> this is main
> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.

> But with ES modules, you’re building up this whole module graph beforehand… before you do any evaluation. This means you can’t have variables in your module specifiers, because those variables don’t have values yet.

CommonJS 模組是指需求方只要以JS檔案來執行其模組，其模組本身是透過執行模組期間輸出模組內容至需求方，所以由於透過執行來獲取模組內容，所以本身可以透過執行狀況來變更其他要被載入的模組

### CommonJS 如何以自身的角度來解決Cyclic Dependency 問題

> Let’s look at how this would work with CommonJS modules. First, the main module would execute up to the require statement. Then it would go to load the counter module.


![](https://hacks.mozilla.org/files/2018/03/41_cyclic_graph-768x432.png)

> The counter module would then try to access `message` from the export object. But since this hasn’t been evaluated in the main module yet, this will return undefined. The JS engine will allocate space in memory for the local variable and set the value to undefined.

![](https://hacks.mozilla.org/files/2018/03/42_cjs_variable_2-768x174.png)


>Evaluation continues down to the end of the counter module’s top level code. We want to see whether we’ll get the correct value for message eventually (after main.js is evaluated), so we set up a timeout. Then evaluation resumes on `main.js`.

![](https://hacks.mozilla.org/files/2018/03/43_cjs_cycle-768x344.png)

> The message variable will be initialized and added to memory. But since there’s no connection between the two, it will stay undefined in the required module.


![](https://hacks.mozilla.org/files/2018/03/44_cjs_variable_2-768x331.png)


重點：
- CommonJS 沒準備手段去面對cyclic dependency問題時，肯定會因為DFS的關係要繞好幾圈，導致無法正常產生模組實例給需求方
- CommonJS解決的概念為：挑出環狀依賴結構上的最後一個會遍歷到的模組並透過移除對於第一個會遍歷到的模組之間的依賴關係來轉換成非環狀依賴結構
	比如說
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659203325/blog/javascript/module/cyclic-dependecy-example_dmfgnv.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659203324/blog/javascript/module/cyclic-dependecy-solution-example_y97fcp.png)

- 最後遍歷到的模組A和第一個會遍歷到的模組B之間的依賴關係移除方式為：
	- 回傳模組B處於evaluation執行之前的模組實例狀態給最後遍歷到的模組就能使模組B移除掉對於模組A之間的依賴
```
const xxx = require(moduleA)
```


## 複習
#🧠 CommonJS 是什麼？->->-> `源自於支援Node.js伺服器端的第三方模組化標準`
<!--SR:!2024-06-06,408,250-->

#🧠 CommonJS 是什麼加載？同步？非同步？ ->->-> `目前模組的載入必須等待前面模組的載入階段都完成才能做`
<!--SR:!2024-12-19,519,250-->

#🧠 CommonJS 會用到模組依賴關係圖嗎？主要是用啥 ->->-> `會，主要用來遍歷模組來找到需要處理的模組以及檢測是否發生環狀依賴關係結構`
<!--SR:!2024-08-18,409,230-->

#🧠 CommonJS 是單執行緒來處理嗎？ ->->-> `對`
<!--SR:!2024-01-18,327,250-->


#🧠 當要載入CommonJS模組時，會如何挑依賴模組以及挑到了要做什麼？->->-> `會透過DFS Post-Order Traversal來從模組依賴關係圖中挑出沒依賴其他模組的模組或者依賴著已經處理完模組加載的模組，並對那個模組進行一次性的獲取&建構、實例化、執行evaluation，最後再將模組實例所要輸出的內容回傳至需求方`
<!--SR:!2023-11-12,280,250-->

#🧠 當需求方以require來載入CommonJS模組時，具體會做什麼樣的載入？->->-> `這時JS引擎會先於編譯期間做： - 分配記憶體空間給模組下的模組實例module物件、var變數宣告、函式宣告 - 分配初始值給var變數為undefined、函式宣告會是拿到存放函式內容的記憶體區塊、模組實例(exports部分會是{} ) - 建立EC來紀錄模組下的每個識別字和對應實體物件，接著在執行該模組的top-level code 來產生模組要輸出的內容以及執行輸出模組內容的語句，如：執行到下列語句才會把輸出內容從空物件轉換成指定內容最後再將模組實例所要輸出的內容回傳至需求方`
<!--SR:!2024-03-24,257,210-->

#🧠 當需求方以require來載入CommonJS模組時，JS引擎在編譯時的Bytecode會做什麼？->->-> `- 分配記憶體空間給模組下的模組實例module物件、var變數宣告、函式宣告 - 分配初始值給var變數為undefined、函式宣告會是拿到存放函式內容的記憶體區塊、模組實例(exports部分會是{} ) - 建立EC來紀錄模組下的每個識別字和對應實體物件`
<!--SR:!2023-10-30,103,230-->

#🧠 當需求方以require來載入CommonJS模組時，會如何定義exports的初始值->->-> `給予{}`
<!--SR:!2024-11-25,511,250-->

``

#🧠 當需求方以require來載入CommonJS模組時，如何確定exports的最終值？ ->->-> `執行module.exports =...，就能確定exports的最終值`
<!--SR:!2025-02-18,518,230-->

#🧠 請畫圖來表示實例是如何分配給需求方，當需求方以require來載入CommonJS模組時執行exports和回傳需求方的require ->->-> `![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)`
<!--SR:!2024-02-04,337,250-->

#🧠 CommonJS 完成實例化並回傳需求方的require會是指什麼？ 模組實例本身嗎？->->-> `會直接拿到模組實例的副本`
<!--SR:!2025-01-07,539,250-->

#🧠 CommonJS模組：main 模組依賴著M1模組、M2模組、M3模組；M1 模組依賴M4 模組、M5模組；M2 模組依賴M6模組，那麼當載入main模組時，JS引擎會如何處理？順序是什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659287023/blog/javascript/module/commonjs-module-example_vovrps.png) ->->-> `首先一開始從main.js執行，並且為了載入module1而執行對應Module1模組來獲取對應模組輸出內容，接著module1模組在一開始表明依賴著module4，所以就轉而去執行module4來獲取其模組輸出內容，由於Module4模組沒再依賴任何模組，所以就直接印出this is module4並輸出指定 內容給module1當module4所參照的物件，接著執行權就從M4回轉至M1，並由M1來執行module5來獲取對應輸出內容，而module5並沒有任何依賴模組的需求就直接印出this is module5 並輸出指定內容給M1，接著執行權回到M1，M1已經載入完成，就印出this is module1，接著就輸出自己模組的內容至main模組所要參照的模組物件。 執行權回到main.js，並轉由執行module2來獲取其模組輸出內容，而module2依賴著Module6，因而執行module6來獲取其模組輸出內容，module6並沒有依賴模組，所以就執行印出this is module6，然後就輸出模組內容至module2當參照物件，接著執行權回到M2，M2也載入所有依賴模組，就直接印出this is module2，接著輸出自己模組內容至main.js當參照內容，執行權回到main.js，而main.js此時只剩module3還未載入，就執行Module3來獲取對應模組內容，module3本身沒有依賴模組，所以只需要執行印出this is module3，然後輸出自己模組內容至main.js當參照物件，最後執行權回到main.js，main.js也載入所有依賴模組，這時就會執行main.js的內容，也就是this is main。所以順序會是：this is module 4 -> this is module 5 -> this is module 1 -> this is module 6 -> this is module 2 -> this is module 3 -> this is main`
<!--SR:!2024-02-05,201,230-->

#🧠 CommonJS 模組若沒有手段去面對cyclic dependency問題時，會出現什麼樣的問題？ ->->-> `肯定會因為DFS的關係要繞好幾圈，導致無法正常產生模組實例給需求方`
<!--SR:!2024-04-22,380,250-->

#🧠 CommonJS 模組是如何面對cyclic dependency問題？（概念上)->->-> `挑出環狀依賴結構上的最後一個會遍歷到的模組並透過移除對於第一個會遍歷到的模組之間的依賴關係來轉換成非環狀依賴結構`
<!--SR:!2024-12-31,532,250-->

#🧠 CommonJS 模組是如何面對cyclic dependency問題？具體是如何幫最後一個會遍歷到的模組移除對於第一個會遍歷到的模組之間的依賴關係來轉換成非環狀依賴結構 ->->-> `回傳模組1處於evaluation執行之前的模組實例狀態給最後1個遍歷到的模組就能使最後1個遍歷到的模組移除掉對於模組1之間的依賴`
<!--SR:!2024-05-31,406,250-->


#🧠 以三個環狀依賴結構為例子，來說明CommonJS 模組是如何面對cyclic dependency問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659203325/blog/javascript/module/cyclic-dependecy-example_dmfgnv.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659203324/blog/javascript/module/cyclic-dependecy-solution-example_y97fcp.png)`
<!--SR:!2024-12-28,535,250-->



#🧠 用下圖來說明如何解決cyclic dependency問題，在這裏main.js和counter.js互為依賴，並且先執行main.js，其中setTimeout任務的執行順序會是如何？會是印出什麼？![](https://hacks.mozilla.org/files/2018/03/43_cjs_cycle-500x224.png) ->->-> `由於call stack還有module的載入和執行，所以非同步任務放到最後，counter undefined -> main 5 -> async task undefined`
<!--SR:!2024-02-10,201,247-->


#🧠 用下圖來說明如何解決cyclic dependency問題，在這裏main.js和counter.js互為依賴，並且先執行main.js![counter.js returning control to main.js, which finishes evaluating](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/43_cjs_cycle-500x224.png) ->->-> `一開始會先使用檢測環狀依賴結構的算法來判定，在這裡是能夠確定，所以會將counter.js對於main.js的依賴關係給移除。剛開始執行main.js時，會於編譯時期替main.js分配記憶體空間來建立實例，同時預設設定{}至module.exports，接著在建立EC來替每個識別字能夠對應其實體物件，接著就進入執行來調用counter.js模組，然後就跑到counter.js那邊進行編譯時的實例化和設定，在執行時會直接碰到對於main.js的require，在這裏由於是被算法指定要移除，所以會直接獲取main.js那邊還未執行evaluation來確定值的版本，所以message會是undefined，並接著繼續執行counter.js的top-level code並確定要輸出的內容為count = 5，執行完畢之後，就跳回main.js那邊，將5回傳給count，讓main.js去印以及去設定message的最終值為Eval complete。`
<!--SR:!2024-01-11,318,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[環狀依賴結構會是指多個模組因為彼此依賴而在依賴關係上構成多個模組構成的環狀依賴結構]]
References: