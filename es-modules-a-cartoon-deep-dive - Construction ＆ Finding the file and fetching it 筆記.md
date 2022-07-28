


## 描述

#### Construction

> Three things happen for each module during the Construction phase.
> 
> 1.  Figure out where to download the file containing the module from (aka module resolution)
> 2.  Fetch the file (by downloading it from a URL or loading it from the file system)
> 3.  Parse the file into a module record


在建構階段中，瀏覽器會替每個模組做三件事情：

-   解析模組在哪裡可以載入
-   從指定地址獲取對應模組
-   解析模組成module record

#### Finding the file and fetching it

> The loader will take care of finding the file and downloading it. First it needs to find the entry point file. In HTML, you tell the loader where to find it by using a script tag.

[![A script tag with the type=module attribute and a src URL. The src URL has a file coming from it which is the entry](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/08_script_entry-500x188.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/08_script_entry.png)

> But how does it find the next bunch of modules — the modules that `main.js` directly depends on?

> This is where import statements come in. One part of the import statement is called the module specifier. It tells the loader where it can find each next module.

[![An import statement with the URL at the end labeled as the module specifier](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/09_module_specifier-500x105.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/09_module_specifier.png)

> One thing to note about module specifiers: they sometimes need to be handled differently between browsers and Node. Each host has its own way of interpreting the module specifier strings. To do this, it uses something called a module resolution algorithm, which differs between platforms. Currently, some module specifiers that work in Node won’t work in the browser, but there is [ongoing work to fix this](https://github.com/domenic/package-name-maps).

關於module specifier的細節：

1.  module specifier 可以是使用URL、本地端的相對路徑和絕對路徑
2.  有時ES module會用在瀏覽器和伺服器端
3.  每個平台各有自己的方法來解析module specifier

為了統一各平台對於module specifier的解析，有人就提出module resolution algorithm，能根據平台來以不同的方式解析

> Until that’s fixed, browsers only accept URLs as module specifiers. They will load the module file from that URL. But that doesn’t happen for the whole graph at the same time. You don’t know what dependencies the module needs you to fetch until you’ve parsed the file… and you can’t parse the file until you fetched it.

> This means that we have to go through the tree layer-by-layer, parsing one file, then figuring out its dependencies, and then finding and loading those dependencies.

瀏覽器會使用URL作為module specifier，模組的依賴關係會從從對應主機獲取(fetch)對應main.js模組，然後解析成對應module record來找到main.js模組依賴的模組是哪些，然後再從模組的module specifier找對對應主機獲取(fetch)對應依賴模組，接著在解析成對應module record，找到是否有依賴模組。

[![A diagram that shows one file being fetched and then parsed, and then two more files being fetched and then parsed](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/10_construction-500x302.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/10_construction.png)

> If the main thread were to wait for each of these files to download, a lot of other tasks would pile up in its queue.
> 
> That’s because when you’re working in a browser, the downloading part takes a long time.

![A chart of latencies showing that if a CPU cycle took 1 second, then main memory access would take 6 minutes, and fetching a file from a server across the US would take 4 years](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/11_latency-500x270.png)  



> But unlike function scopes, module scopes have a way of making their variables available to other modules as well. They can say explicitly which of the variables, classes, or functions in the module should be available. 
  
module scope 主要是指特定模組下的識別空間，該空間會有變數、函式、類別，且他們皆能透過同一個識別空間而共享。

> When something is made available to other modules, it’s called an export. Once you have an export, other modules can explicitly say that they depend on that variable, class or function. 

export：模組A輸出模組A下的特定函式或者變數至其他模組B使用  
  
一旦你指定哪些是模組要輸出的，其他模組可以很清楚地知道它們所依賴的變數、類別、函式是對應著什麼以及源自於哪裡？

> Because this is an explicit relationship, you can tell which modules will break if you remove another one. 


因爲可以明確告知哪些變數、函式、類別源自於哪且又是什麼，所以若不想特定變數、函式、類別的話，可以以明確的方式來告知。

> Today there are two module systems that are actively being used. CommonJS (CJS) is what Node.js has used historically. ESM (EcmaScript modules) is a newer system which has been added to the JavaScript specification. Browsers already support ES modules, and Node is adding support. 


現存所流行的模組標準分別為CommonJS (CJS)是源自於Node.js，而EcmaScript modules (ESM) 是一個新的標準，目前已經增加至ECMAScript標準，大部分瀏覽器都支援，但Node.js仍在持續支援著，並不能說是完全支援(by 2018)

> When you’re developing with modules, you build up a graph of dependencies. The connections between different dependencies come from any import statements that you use.
> 
 > These import statements are how the browser or Node knows exactly what code it needs to load. You give it a file to use as an entry point to the graph. From there it just follows any of the import statements to find the rest of the code. 
 > 
 > After that, the module record needs to be turned into a module instance. An instance combines two things: the code and state. 


![](https://hacks.mozilla.org/files/2018/03/05_module_record-768x441.png)
 
module record ：
1.  會轉換成module instance
2.  一個module instance 會將code和state結合在一塊

> The code is basically a set of instructions. It’s like a recipe for how to make something. But by itself, you can’t use the code to do anything. You need raw materials to use with those instructions. 

code 基本是做某件事情的一組指令，在這裡會是指依賴模組所匯出來的功能函式內容

> What is state? State gives you those raw materials. State is the actual values of the variables at any point in time. Of course, these variables are just nicknames for the boxes in memory that hold the values. 

state 則是代表著特定時機點下特定變數所擁有的實際值，也就是所有變數值。在這裡變數只不過用來稱呼並區分這些存放實際值的記憶體區塊，state為每個用識別字對應的記憶體區塊

> What we need is a module instance for each module. The process of module loading is going from this entry point file to having a full graph of module instances. 

每一個模組為一個module instance ，模組管理最主要會由一個模組來管理全部可能依賴的模組，並由那個模組開始解析目前可能依賴的模組並生成對應的module instance

![](https://hacks.mozilla.org/files/2018/03/06_module_instance-768x572.png)

> For ES modules, this happens in three steps.
> 
> Construction： find, download, and parse all of the files into module records.
> 
> Instantiation ：find boxes in memory to place all of the exported values in (but don’t fill them in with values yet). Then make both exports and imports point to those boxes in memory. This is called linking.
> 
> Evaluation ：run the code to fill in the boxes with the variables’ actual values. 

![](https://hacks.mozilla.org/files/2018/03/07_3_phases-768x282.png)

> People talk about ES modules being asynchronous. You can think about it as asynchronous because the work is split into these three different phases — loading, instantiating, and evaluating — and those phases can be done separately. 


ES modules 會是非同步載入，主要是因為：

1.  將每個模組的載入切分出這三個階段並將每個階段視為一個任務：loading(construction)、instantiation、evaluation
2.  同為模組的任務們勢必得得先經歷那些階段的依賴關係，但若考慮到不同模組的任務們則可以與其他模組的任務們保持著非同步的關係，換言之，模組A的每個任務和模組B的每個任務都互為獨立、互不依賴，不會發生每個任務等待前面任務完成才能做的事情

第二個因素必須是在ES module已經先處理好模組間的依賴關係，並優先處理最需要載入的模組，不過仍會發生模組間的依賴關係而使得模組A的部分任務必須等待前面目前執行的模組B部分任務完成才能做。
> but in CJS a module and the dependencies below it are loaded, instantiated, and evaluated all at once, without any breaks in between.
  
  > However, the steps themselves are not necessarily asynchronous. They can be done in a synchronous way. It depends on what’s doing the loading. That’s because not everything is controlled by the ES module spec. There are actually two halves of the work, which are covered by different specs. 
  
Common JS ：

 * 將每個模組的載入分成construction、instantiation、evaluation三個階段
 * 每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做

> The ES module spec says how you should parse files into module records, and how you should instantiate and evaluate that module. However, it doesn’t say how to get the files in the first place.
> 
 > It’s the loader that fetches the files. And the loader is specified in a different specification. For browsers, that spec is the HTML spec. But you can have different loaders based on what platform you are using. 
 
 ![](https://hacks.mozilla.org/files/2018/03/07_loader_vs_es-768x439.png)
ES Module 標準是說程式該如何解析ES模組成模組紀錄以及如何實例化、確定值，然而它卻沒制定一個標準來定義在一開始的模組載入中，如何獲取檔案/ES模組。

這對於模組載入來說，獲取檔案/ES模組會是載入階段中的首要任務，通常瀏覽器會建立loader來負責\*\*_載入各種檔案，並從而根據檔案種類來進行處理以及對於模組的載入工作_\*\*，然而每一個瀏覽器的loader都基於不同的標準，通常會採用於HTML spec，該標準會使用自己內定的模組載入方式來處理，若採用不同標準的loader來載入ES模組，很有可能無法如同ECAMScript標準那樣實現模組載入

> The loader also controls exactly how the modules are loaded. It calls the ES module methods — ParseModule, Module.Instantiate, and Module.Evaluate. It’s kind of like a puppeteer controlling the JS engine’s strings. 

![](https://hacks.mozilla.org/files/2018/03/08_loader_as_puppeteer-768x507.png)


瀏覽器會為了能夠處理ES模組，會將支援ES module spec - 如何解析、實例化、確定/判定值這些階段處理的實現納入至基於HTML spec的loader改造成當載入ES模組時，就呼叫對應方法來做每個模組下的階段任務

> Three things happen for each module during the Construction phase.
> - Figure out where to download the file containing the module from (aka module resolution)
> - Fetch the file (by downloading it from a URL or loading it from the file system)
> - Parse the file into a module record 


在建構階段中，瀏覽器會替每個模組做三件事情：

 * 解析模組在哪裡可以載入
 * 從指定地址獲取對應模組
 * 解析模組成module record



## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@wikidataEvaluationDisambiguation2022]]