
## 描述

[[@linclarkESModulesCartoon]]  所描述：
> This means the spec does introduce a kind of asynchrony that wasn’t there in CommonJS. I’ll explain more later, but in CJS a module and the dependencies below it are loaded, instantiated, and evaluated all at once, without any breaks in between.

> However, the steps themselves are not necessarily asynchronous. They can be done in a synchronous way. It depends on what’s doing the loading. That’s because not everything is controlled by the ES module spec. There are actually two halves of the work, which are covered by different specs.

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段(在這裡CommonJS並不會特意分割這三個階段)
-   每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做


This approach—having the algorithm split up into phases—is one of the key differences between ES modules and CommonJS modules.

> CommonJS can do things differently because loading files from the filesystem takes much less time than downloading across the Internet. This means Node can block the main thread while it loads the file. And since the file is already loaded, it makes sense to just instantiate and evaluate (which aren’t separate phases in CommonJS). This also means that you’re walking down the whole tree, loading, instantiating, and evaluating any dependencies before you return the module instance.

CommonJS 本身是源自於伺服器端的模組化標準，其模組皆源自於伺服器本機端，只考量如從硬碟獲取對應模組內容並載入至特定區塊，所以並沒有考量網路上的傳輸延遲問題，網路上的傳輸延遲會比從本機端獲取模組來得慢。

因此CommonJS設計上會是：

1.  以模組在本機端儲存設備上為前提
    
2.  獲取模組A以及載入模組A的方式是同步(以建構、實例化、確定值這些階段來說)：在儲存設備找到模組A→ 將模組A轉化成實例 → 執行模組A內的代碼並試著透過執行來載入它所依賴的模組B → 執行模組A所要執行的程式碼 → 回傳模組A實例至需要載入的那一方
    
3.  沒特意將模組載入細分成建構、實例化、確定值這幾個階段
    
4.  模組的依賴關係遍歷會是DFS

[![A diagram showing a Node module evaluating up to a require statement, and then Node going to synchronously load and evaluate the module and any of its dependencies](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/12_cjs_require-500x298.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/12_cjs_require.png)

> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.

> But with ES modules, you’re building up this whole module graph beforehand… before you do any evaluation. This means you can’t have variables in your module specifiers, because those variables don’t have values yet.

CommonJS 模組是指需求方只要以JS檔案來執行其模組，其模組本身是透過執行模組期間輸出模組內容至需求方，所以由於透過執行來獲取模組內容，所以本身可以透過執行狀況來變更其他要被載入的模組

而ES 模組 本身是在主程式和模組這兩者的編譯/解析期間就載入模組內容至需求方，所以在真正模組執行的時候就已經按照定義好的依賴關係(順序)來執行，換言之，本身無法在執行期間透過執行狀態來改變載入模組


[![A require statement which uses a variable is fine. An import statement that uses a variable is not.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import-500x146.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import.png)




> This is different from CommonJS modules. In CommonJS, the entire export object is copied on export. This means that any values (like numbers) that are exported are copies.

> This means that if the exporting module changes that value later, the importing module doesn’t see that change.

commonJS 模組A的實例化也是存放在記憶體，當需求方想要載入commonJS 模組A時，就複製存放記憶體內的實例並將副本放置另一個記憶體區塊任由需求方去存取，這時會有兩個記憶體分別存放著commonJS模組A和commonJS模組A副本

![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)





> What about those cycles that we talked about before?
> 
> In a cyclic dependency, you end up having a loop in the graph. Usually, this is a long loop. But to explain the problem, I’m going to use a contrived example with a short loop.

[![A complex module graph with a 4 module cycle on the left. A simple 2 module cycle on the right.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cjs_cycle-500x224.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cjs_cycle.png)

> Let’s look at how this would work with CommonJS modules. First, the main module would execute up to the require statement. Then it would go to load the counter module.

[![A commonJS module, with a variable being exported from main.js after a require statement to counter.js, which depends on that import](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cyclic_graph-500x281.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/41_cyclic_graph.png)

> The counter module would then try to access `message` from the export object. But since this hasn’t been evaluated in the main module yet, this will return undefined. The JS engine will allocate space in memory for the local variable and set the value to undefined.

[![Memory in the middle with no connection between main.js and memory, but an importing link from counter.js to a memory location which has undefined](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/42_cjs_variable_2-500x113.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/42_cjs_variable_2.png)

> Evaluation continues down to the end of the counter module’s top level code. We want to see whether we’ll get the correct value for message eventually (after main.js is evaluated), so we set up a timeout. Then evaluation resumes on `main.js`.

[![counter.js returning control to main.js, which finishes evaluating](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/43_cjs_cycle-500x224.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/43_cjs_cycle.png)

> The message variable will be initialized and added to memory. But since there’s no connection between the two, it will stay undefined in the required module.

**[![main.js getting its export connection to memory and filling in the correct value, but counter.js still pointing to the other memory location with undefined in it](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/44_cjs_variable_2-500x216.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/44_cjs_variable_2.png)**




## 複習
---
Status: 
Tags:
[[JavaScript]]
Links:

References:
[[@linclarkESModulesCartoon]]