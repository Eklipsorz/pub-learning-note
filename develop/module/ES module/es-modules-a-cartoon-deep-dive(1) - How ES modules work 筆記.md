
## 描述


> When you’re developing with modules, you build up a graph of dependencies. The connections between different dependencies come from any import statements that you use.

> These import statements are how the browser or Node knows exactly what code it needs to load. You give it a file to use as an entry point to the graph. From there it just follows any of the import statements to find the rest of the code.


以一個模組檔案來控管專案中所要使用的模組，具體會先以main.js模組檔案來建立模組依賴關係圖(graph)的起始點，並由該節點的子節點來做為專案最一開始想要載入的模組，起始點與子節點之間關係會是起始點會依賴著代表子節點的模組，若代表子節點A的模組本身依賴其他模組的話，就以它為根節點來衍生出子節點B來表示子節點A的模組所依賴的模組，後續節點的關係就以這個作為展開

比如說：專案最一開始想要載入counter.js和display.js，在這裡建立main.js來控管他們，以main.js作為依賴counter.js模組和display.js模組的模組來構成模組依賴關係圖(graph)

[![A module with two dependencies. The top module is the entry. The other two are related using import statements](https://hacks.mozilla.org/files/2018/03/04_import_graph-768x447.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/04_import_graph.png)

> But files themselves aren’t something that the browser can use. It needs to parse all of these files to turn them into data structures called Module Records. That way, it actually knows what’s going on in the file.

在構築模組依賴關係圖(graph)的過程中，會先將一個模組簡化成模組紀錄，然後再透過模組紀錄得知該模組所依賴的模組

模組紀錄

> 把解析出来的模块构成表 称为 Module Record（模块记录）。  Module Record 包含了当前模块的 AST，引用了哪些模块的变量，以及一些特定属性和方法。

[![A module record with various fields, including RequestedModules and ImportEntries](https://hacks.mozilla.org/files/2018/03/05_module_record-768x441.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/05_module_record.png)

> After that, the module record needs to be turned into a module instance. An instance combines two things: the code and state.

組建成模組依賴關係圖後，就會將每個模組紀錄(module record)轉換成每一個模組實例(module instance)，每個模組實例會含有code 和 state 這兩大主要內容

> The code is basically a set of instructions. It’s like a recipe for how to make something. But by itself, you can’t use the code to do anything. You need raw materials to use with those instructions.

code 基本是做某件事情的一組指令，在這裡會是指模組要進行evaluation時的code

> What is state? State gives you those raw materials. State is the actual values of the variables at any point in time. Of course, these variables are just nicknames for the boxes in memory that hold the values.

state 則是代表著特定時機點下特定變數所擁有的實際值，也就是模組下所有識別字所對應的記憶體區塊所存的內容

> So the module instance combines the code (the list of instructions) with the state (all the variables’ values).

[![A module instance combining code and state](https://hacks.mozilla.org/files/2018/03/06_module_instance-768x572.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/06_module_instance.png)

> What we need is a module instance for each module. The process of module loading is going from this entry point file to having a full graph of module instances.

每一個模組為一個module instance

模組管理最主要會由一個模組來管理全部可能依賴的模組，並由那個模組開始解析目前可能依賴的模組並生成對應的module instance

> For ES modules, this happens in three steps.

> 1.  Construction — find, download, and parse all of the files into module records.
> 2.  Instantiation —find boxes in memory to place all of the exported values in (but don’t fill them in with values yet). Then make both exports and imports point to those boxes in memory. This is called linking.
> 3.  Evaluation —run the code to fill in the boxes with the variables’ actual values.

ES module 在模組的載入上具體有三個步驟：

-   建構階段：主要會去解讀模組所在的主機(位置)、並且向該主機索要模組、然後將模組解析成module record、接著再另外依據import/export來建立模組依賴關係圖
-   模組實例化：需等待所有模組的建構階段完成，遍歷模組依賴關係圖來找到不需要載入模組或者載入已經完成實例化的模組進行記憶體分配，其記憶體會是存放模組輸出的內容，會是以識別字對應著特定記憶體區塊，其初始值會按照函式宣告/var/const宣告規則來給定、對每個模組的import/export都能指向對應特定模組的識別字所指向的記憶體區塊
-   執行模組內容並確定模組實例的輸出內容：當做完實例化之後，就執行對應代碼並根據識別字來更新對應記憶體區塊存放的內容

在這裏，模組實例化就已經確保其模組已經載入，並開始供其他模組使用並透過evaluation來確定模組下的每個識別字對應的記憶體區塊存放內容


[![The three phases. Construction goes from a single JS file to multiple module records. Instantiation links those records. Evaluation executes the code.](https://hacks.mozilla.org/files/2018/03/07_3_phases-768x282.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_3_phases.png)

> People talk about ES modules being asynchronous. You can think about it as asynchronous because the work is split into these three different phases — loading, instantiating, and evaluating — and those phases can be done separately.

ES modules 會是非同步，主要是因為：

1.  將每個模組的載入切分出這三個階段並將每個階段視為一個任務：loading/fetch(construction)、instantiation、evaluation
    
2.  同為模組的任務們勢必得得先經歷那些階段的依賴關係，但若考慮到不同模組的任務們則可以與其他模組的任務們保持著非同步的關係，換言之，模組A的每個任務和模組B的每個任務都互為獨立、互不依賴，不會發生每個任務等待前面任務完成才能做的事情
    

第二個因素必須是在ES module已經先處理好模組間的依賴關係，並優先處理依賴程度較低的模組，不過仍會發生模組間的依賴關係而使得模組A的部分任務必須等待前面目前執行的模組B部分任務完成才能做。

> This means the spec does introduce a kind of asynchrony that wasn’t there in CommonJS. I’ll explain more later, but in CJS a module and the dependencies below it are loaded, instantiated, and evaluated all at once, without any breaks in between.

> However, the steps themselves are not necessarily asynchronous. They can be done in a synchronous way. It depends on what’s doing the loading. That’s because not everything is controlled by the ES module spec. There are actually two halves of the work, which are covered by different specs.

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段(在這裡CommonJS並不會特意分割這三個階段)
-   每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做

> The [ES module spec](https://tc39.github.io/ecma262/#sec-modules) says how you should parse files into module records, and how you should instantiate and evaluate that module. However, it doesn’t say how to get the files in the first place.

> It’s the loader that fetches the files. And the loader is specified in a different specification. For browsers, that spec is the [HTML spec](https://html.spec.whatwg.org/#fetch-a-module-script-tree). But you can have different loaders based on what platform you are using.

ES Module 標準是說程式該如何解析ES模組成模組紀錄、如何實例化、確定值，然而它卻沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組。

這對於模組載入來說，獲取檔案/ES模組會是載入階段中的首要任務，通常瀏覽器會建立loader來負責載入各種檔案，並從而根據檔案種類來進行處理以及對於模組的載入工作，然而每一個瀏覽器的loader都基於不同的標準，通常會採用於HTML spec，該標準會使用自己內定的模組載入方式來處理，若採用不同標準的loader來載入ES模組，很有可能無法如同ECAMScript標準那樣實現模組載入


[![Two cartoon figures. One represents the spec that says how to load modules (i.e., the HTML spec). The other represents the ES module spec.](https://hacks.mozilla.org/files/2018/03/07_loader_vs_es-768x439.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/07_loader_vs_es.png)

> The loader also controls exactly how the modules are loaded. It calls the ES module methods — `ParseModule`, `Module.Instantiate`, and `Module.Evaluate`. It’s kind of like a puppeteer controlling the JS engine’s strings.


瀏覽器會為了能夠處理ES模組，會將支援ES module spec - 如何解析、實例化、確定/判定值這些階段處理的實現納入至基於HTML spec的loader改造成當載入ES模組時，就呼叫對應方法來做每個模組下的階段任務

[![The loader figure acting as a puppeteer to the ES module spec figure.](https://hacks.mozilla.org/files/2018/03/08_loader_as_puppeteer-768x507.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/08_loader_as_puppeteer.png)


## 複習

#🧠 ES module 的載入會需要哪三個步驟來完成？->->-> `建構階段、模組實例化、執行模組內容並確定模組實例的輸出內容`


#🧠 以這個圖示來說明如何執行ES module載入中的哪三個步驟 ![A module with two dependencies. The top module is the entry. The other two are related using import statements](https://hacks.mozilla.org/files/2018/03/04_import_graph-768x447.png)  ->->-> ``


#🧠 ES module 的載入： 建構階段中會做什麼 ->->-> `主要會去解讀模組所在的位置、並且向該位置索要模組、然後將模組解析成module record、接著再另外依據import/export來建立模組依賴關係圖`


#🧠 ES module 的載入：(如何挑選和實例化) 模組實例化是會做什麼？ ->->-> `遍歷模組依賴關係圖來找到不需要載入模組或者載入已經完成實例化的模組進行記憶體分配，其記憶體會是存放模組輸出的內容，會是以識別字對應著特定記憶體區塊，其初始值會按照函式宣告/var/const宣告規則來給定、對每個模組的import/export都能指向對應特定模組的識別字所指向的記憶體區塊`



#🧠 ES module 的載入：模組實例化是會做什麼？ ->->-> `遍歷模組依賴關係圖來找到不需要載入模組或者載入已經完成實例化的模組進行記憶體分配，其記憶體會是存放模組輸出的內容，會是以識別字對應著特定記憶體區塊，其初始值會按照函式宣告/var/const宣告規則來給定、對每個模組的import/export都能指向對應特定模組的識別字所指向的記憶體區塊`



#🧠 ES module 的載入： 模組實例化要做之前，等待什麼？->->-> `等待建構階段完成`


#🧠 ES module 的載入： 確定全部模組要做evaluation之前，等待什麼->->-> `等待所有模組的實例化是否完成，完成就繼續`



#🧠 ES module Evaluation： 執行模組內容之後，實際會是對識別字的記憶體區塊做了什麼？ ->->-> `透過執行模組內的top-level code來更新每個識別字對應的記憶體區塊所存的內容`



#🧠 ES module的載入：每個實例會有哪兩大內容，具體做什麼？->->-> `code 和 state 這兩大主要內容。code 基本是做某件事情的一組指令，在這裡會是指模組要進行evaluation時的code、state 則是代表著特定時機點下特定變數所擁有的實際值，也就是模組下所有識別字所對應的記憶體區塊所存的內容`




#🧠 ES module 以模組實例化和它之前的建構來舉例非同步的任務如何做？(提示，記得要等待)->->-> `在做實例化之前，必須等待所有模組的建構都完成，才能做。不同模組的任務可以不必等待不同模組的任務，會依據著模組依賴圖來對不需要載入模組或者載入已經完成實例化的模組進行記憶體分配，不同模組的實例化任務並不會等待其他模組的實例化任務`



#🧠 ES module 以執行模組內容並確定模組實例的輸出內容和實例化之間的執行關係，請舉例來說明非同步的任務如何做(提示，記得要等待) ->->-> `在做evaluation之前，必須等待所有模組的實例都完成才能做。不同模組的任務可以不必等待不同模組的任務，會依據著模組依賴圖來對不需要模組或者載入已經完成evaluation的模組進行evaluation`


#🧠 ES Module 標準主要是對模組做什麼？ ->->-> `ES Module 標準是說程式該如何解析ES模組成模組紀錄、如何實例化、確定值`




#🧠 ES Module 標準有說如何在一開始的模組載入中獲取檔案/ES模組嗎->->-> `沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組`


#🧠 ES Module 標準沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組，這會發生什麼？ 會對ES模組產生影響嗎？->->-> `各個瀏覽器和伺服器平台皆會以自己的載入標準來處理，部分規則很有可能沒辦法執行ES模組的解析、實例化、確定`


#🧠 瀏覽器的loader是做什麼？ ->->-> `負責解析檔案所在的位置、根據位置來下載檔案、根據檔案種類來進行處理`



#🧠 ES Module 標準沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組，有可能會對ES模組產生影響，請以瀏覽器的loader來說明 ->->-> `預設會是以HTML spec，直接解析模組所在的主機(位置)、向主機索要對應模組，並載入至本地端`



#🧠 瀏覽器預設的loader會採取什麼標準來實現解析檔案所在、下載檔案、根據檔案種類來做處理？ ->->-> `HTML Spec`



#🧠 若要讓瀏覽器的loader能夠在接收到檔案時就正常ES Module的解析/實例化/確定的話，解決辦法為 ->->-> `將能夠處理ES模組，會將支援ES module spec - 如何解析、實例化、確定/判定值這些階段處理的實現納入至基於HTML spec的loader改造成當載入ES模組時，就呼叫對應方法來做每個模組下的階段任務`



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive(4) - Instantiation 筆記]]
[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
[[es-modules-a-cartoon-deep-dive(3) - Parsing 筆記]]
[[es-modules-a-cartoon-deep-dive(5) - Evaluation 筆記]]
[[es-modules-a-cartoon-deep-dive  - 用語介紹]]
References:
[[@linclarkESModulesCartoon]]