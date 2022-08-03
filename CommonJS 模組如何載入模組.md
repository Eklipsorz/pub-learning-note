## 描述


### 模組載入方式分為三階段

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段(在這裡CommonJS並不會特意分割這三個階段)



### CommonJS源自於伺服器端

CommonJS 本身是源自於伺服器端的模組化標準，由於那時其模組皆源自於伺服器本機端，只考量如從硬碟獲取對應模組內容並載入至特定區塊，所以並沒有考量網路上的傳輸延遲問題，網路上的傳輸延遲會比從本機端獲取模組來得慢。

### 是否擁有模組依賴關係圖

1. 模組加載本身不會有多個執行緒去幫忙加載，只會有一個執行緒進行加載
2. 模組加載是同步加載：每一個模組的加載都必須等待前一個模組的加載完成才能做
3. 每個模組的加載任務內容會是一次做完construction、instantiation、evaluation這三階段

整體來說只需要 stack ＋ DFS post-order traversal 就能實現優先挑選沒依賴任何模組的模組或者依賴著已經完成加載之模組的模組


### 單個CommonJS模組的載入
> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.


[![A require statement which uses a variable is fine. An import statement that uses a variable is not.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import-500x146.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import.png)

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

因此CommonJS設計上會是：

1.  以模組在本機端儲存設備上為前提而設計
2.  同步加載：每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做
3.  載入形式：透過執行模組來載入模組實例至需求方
4.  沒特意將模組載入細分成建構、實例化、確定值這幾個階段，而是會透過DFS遍歷模組依賴關係的底部模組，優先從沒依賴其他模組的模組進行執行並實例化，接著再從依賴完成實例化的模組之模組執行並實例化，後面依此類推
6.  模組的依賴關係遍歷圖會根據require/export這些識別字來構成，從而解決cyclic dependency


### DFS遍歷模組依賴關係例子
依賴模組：
1. main 模組依賴著M1模組、M2模組、M3模組
2. M1 模組依賴M4 模組、M5模組
3. M2 模組依賴M6模組


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659287023/blog/javascript/module/commonjs-module-example_vovrps.png)


首先一開始從main.js執行，並且為了載入module1而執行對應Module1模組來獲取對應模組輸出內容，接著module1模組在一開始表明依賴著module4，所以就轉而去執行module4來獲取其模組輸出內容，由於Module4模組沒再依賴任何模組，所以就直接印出this is module4並輸出指定
內容給module1當module4所參照的物件，接著執行權就從M4回轉至M1，並由M1來執行module5來獲取對應輸出內容，而module5並沒有任何依賴模組的需求就直接印出this is module5 並輸出指定內容給M1，接著執行權回到M1，M1已經載入完成，就印出this is module1，接著就輸出自己模組的內容至main模組所要參照的模組物件。

執行權回到main.js，並轉由執行module2來獲取其模組輸出內容，而module2依賴著Module6，因而執行module6來獲取其模組輸出內容，module6並沒有依賴模組，所以就執行印出this is module6，然後就輸出模組內容至module2當參照物件，接著執行權回到M2，M2也載入所有依賴模組，就直接印出this is module2，接著輸出自己模組內容至main.js當參照內容，執行權回到main.js，而main.js此時只剩module3還未載入，就執行Module3來獲取對應模組內容，module3本身沒有依賴模組，所以只需要執行印出this is module3，然後輸出自己模組內容至main.js當參照物件，最後執行權回到main.js，main.js也載入所有依賴模組，這時就會執行main.js的內容，也就是this is main。

所以順序會是：this is module 4 -> this is module 5 -> this is module 1 -> this is module 6 ->

this is module 2 -> this is module 3 -> this is main
> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.

> But with ES modules, you’re building up this whole module graph beforehand… before you do any evaluation. This means you can’t have variables in your module specifiers, because those variables don’t have values yet.

CommonJS 模組是指需求方只要以JS檔案來執行其模組，其模組本身是透過執行模組期間輸出模組內容至需求方，所以由於透過執行來獲取模組內容，所以本身可以透過執行狀況來變更其他要被載入的模組

### CommonJS 如何以自身的角度來解決Cyclic Dependency 問題

> Let’s look at how this would work with CommonJS modules. First, the main module would execute up to the require statement. Then it would go to load the counter module.

[![A commonJS module, with a variable being exported from main.js after a require statement to counter.js, which depends on that import](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cyclic_graph-500x281.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cyclic_graph.png)

> The counter module would then try to access `message` from the export object. But since this hasn’t been evaluated in the main module yet, this will return undefined. The JS engine will allocate space in memory for the local variable and set the value to undefined.

[![Memory in the middle with no connection between main.js and memory, but an importing link from counter.js to a memory location which has undefined](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/42_cjs_variable_2-500x113.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/42_cjs_variable_2.png)

Evaluation continues down to the end of the counter module’s top level code. We want to see whether we’ll get the correct value for message eventually (after main.js is evaluated), so we set up a timeout. Then evaluation resumes on `main.js`.

[![counter.js returning control to main.js, which finishes evaluating](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/43_cjs_cycle-500x224.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/43_cjs_cycle.png)

> The message variable will be initialized and added to memory. But since there’s no connection between the two, it will stay undefined in the required module.

**[![main.js getting its export connection to memory and filling in the correct value, but counter.js still pointing to the other memory location with undefined in it](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/44_cjs_variable_2-500x216.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/44_cjs_variable_2.png)**



[[環狀依賴結構會是指多個模組因為彼此依賴而在依賴關係上構成多個模組構成的環狀依賴結構]]

- 解法：
	- 先使用DFS為主的環狀依賴偵測算法
	- 若算法得出有循環，就以最後一個從未遍歷的模組作為最後一個模組，最後一個模組
	- 若算法得出沒循環，就結束


## 複習
``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:

References: