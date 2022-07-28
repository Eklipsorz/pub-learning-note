
## 描述


> When you’re developing with modules, you build up a graph of dependencies. The connections between different dependencies come from any import statements that you use.

> These import statements are how the browser or Node knows exactly what code it needs to load. You give it a file to use as an entry point to the graph. From there it just follows any of the import statements to find the rest of the code.

[![A module with two dependencies. The top module is the entry. The other two are related using import statements](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/04_import_graph-500x291.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/04_import_graph.png)

> But files themselves aren’t something that the browser can use. It needs to parse all of these files to turn them into data structures called Module Records. That way, it actually knows what’s going on in the file.


[![A module record with various fields, including RequestedModules and ImportEntries](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/05_module_record-500x287.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/05_module_record.png)

> After that, the module record needs to be turned into a module instance. An instance combines two things: the code and state.

module record ：

1.  會轉換成module instance
2.  一個module instance 會將code和state結合在一塊

> The code is basically a set of instructions. It’s like a recipe for how to make something. But by itself, you can’t use the code to do anything. You need raw materials to use with those instructions.

code 基本是做某件事情的一組指令，在這裡會是指依賴模組所匯出來的功能函式內容

> What is state? State gives you those raw materials. State is the actual values of the variables at any point in time. Of course, these variables are just nicknames for the boxes in memory that hold the values.

state 則是代表著特定時機點下特定變數所擁有的實際值，也就是所有變數值

在這裡變數只不過用來稱呼並區分這些存放實際值的記憶體區塊

state為每個用識別字對應的記憶體區塊

> So the module instance combines the code (the list of instructions) with the state (all the variables’ values).

[![A module instance combining code and state](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/06_module_instance-500x372.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/06_module_instance.png)

> What we need is a module instance for each module. The process of module loading is going from this entry point file to having a full graph of module instances.

每一個模組為一個module instance

模組管理最主要會由一個模組來管理全部可能依賴的模組，並由那個模組開始解析目前可能依賴的模組並生成對應的module instance

> For ES modules, this happens in three steps.

> 1.  Construction — find, download, and parse all of the files into module records.
> 2.  Instantiation —find boxes in memory to place all of the exported values in (but don’t fill them in with values yet). Then make both exports and imports point to those boxes in memory. This is called linking.
> 3.  Evaluation —run the code to fill in the boxes with the variables’ actual values.

ES module 在模組的載入上具體有三個步驟：

-   建構階段：找到、下載、解析對應模組檔案為module records、建構模組依賴關係
-   模組實例化：根據export指定對象來分配記憶體區塊給模組主要輸出的內容存放，並將識別字對應至記憶體區塊，其記憶體區塊內容目前在這階段是空的
-   確定模組實例的內容：執行對應代碼並根據識別字來更新對應記憶體區塊存放的內容

在這裏，模組實例化就已經確保其模組已經載入，並開始供其他模組使用並透過evaluation來確定模組下的每個識別字對應的記憶體區塊存放內容


[![The three phases. Construction goes from a single JS file to multiple module records. Instantiation links those records. Evaluation executes the code.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_3_phases-500x184.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_3_phases.png)

> People talk about ES modules being asynchronous. You can think about it as asynchronous because the work is split into these three different phases — loading, instantiating, and evaluating — and those phases can be done separately.

ES modules 會是非同步載入，主要是因為：

1.  將每個模組的載入切分出這三個階段並將每個階段視為一個任務：loading/fetch(construction)、instantiation、evaluation
    
2.  同為模組的任務們勢必得得先經歷那些階段的依賴關係，但若考慮到不同模組的任務們則可以與其他模組的任務們保持著非同步的關係，換言之，模組A的每個任務和模組B的每個任務都互為獨立、互不依賴，不會發生每個任務等待前面任務完成才能做的事情
    

第二個因素必須是在ES module已經先處理好模組間的依賴關係，並優先處理依賴程度較低的模組，不過仍會發生模組間的依賴關係而使得模組A的部分任務必須等待前面目前執行的模組B部分任務完成才能做。

> This means the spec does introduce a kind of asynchrony that wasn’t there in CommonJS. I’ll explain more later, but in CJS a module and the dependencies below it are loaded, instantiated, and evaluated all at once, without any breaks in between.

> However, the steps themselves are not necessarily asynchronous. They can be done in a synchronous way. It depends on what’s doing the loading. That’s because not everything is controlled by the ES module spec. There are actually two halves of the work, which are covered by different specs.

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段
-   每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做

> The [ES module spec](https://tc39.github.io/ecma262/#sec-modules) says how you should parse files into module records, and how you should instantiate and evaluate that module. However, it doesn’t say how to get the files in the first place.

> It’s the loader that fetches the files. And the loader is specified in a different specification. For browsers, that spec is the [HTML spec](https://html.spec.whatwg.org/#fetch-a-module-script-tree). But you can have different loaders based on what platform you are using.

ES Module 標準是說程式該如何解析ES模組成模組紀錄以及如何實例化、確定值，然而它卻沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組。

這對於模組載入來說，獲取檔案/ES模組會是載入階段中的首要任務，通常瀏覽器會建立loader來負責載入各種檔案，並從而根據檔案種類來進行處理以及對於模組的載入工作，然而每一個瀏覽器的loader都基於不同的標準，通常會採用於HTML spec，該標準會使用自己內定的模組載入方式來處理，若採用不同標準的loader來載入ES模組，很有可能無法如同ECAMScript標準那樣實現模組載入


[![Two cartoon figures. One represents the spec that says how to load modules (i.e., the HTML spec). The other represents the ES module spec.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_loader_vs_es-500x286.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_loader_vs_es.png)

> The loader also controls exactly how the modules are loaded. It calls the ES module methods — `ParseModule`, `Module.Instantiate`, and `Module.Evaluate`. It’s kind of like a puppeteer controlling the JS engine’s strings.


瀏覽器會為了能夠處理ES模組，會將支援ES module spec - 如何解析、實例化、確定/判定值這些階段處理的實現納入至基於HTML spec的loader改造成當載入ES模組時，就呼叫對應方法來做每個模組下的階段任務

[![The loader figure acting as a puppeteer to the ES module spec figure.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/08_loader_as_puppeteer-500x330.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/08_loader_as_puppeteer.png)

## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive - Instantiation 筆記]]
References:
[[@linclarkESModulesCartoon]]