


## 描述

### Construction

> Three things happen for each module during the Construction phase.
> 
> 1.  Figure out where to download the file containing the module from (aka module resolution)
> 2.  Fetch the file (by downloading it from a URL or loading it from the file system)
> 3.  Parse the file into a module record


在建構階段中，瀏覽器會替每個模組做三件事情：

-   解析模組在哪裡可以載入 (地點會是網路或者本地端)
-   從指定地址獲取對應模組 (藉由下載或者從檔案系統載入，更甚至兩者都有)
-   解析模組成module record

最後根據import/export以圖狀資料結構來產生模組依賴關係圖

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


> Blocking the main thread like this would make an app that uses modules too slow to use. This is one of the reasons that the ES module spec splits the algorithm into multiple phases. Splitting out construction into its own phase allows browsers to fetch files and build up their understanding of the module graph before getting down to the synchronous work of instantiating.

瀏覽器的模組源自於以下兩個地方，且效率會侷限於網路和存取設備，一般來說，網路速率會比存取設備還慢：

1.  第三方模組：網路上下載至本地端速率＋從本地端載入檔案至專案的速率
2.  本地端模組：從本地端載入檔案至專案的速率

大部分情況下，由於客戶端所需的模組都是源自第三方，且網路速率會比存取設備還慢，所以會非常依賴於網路速率，所以ES module spec才將模組載入分成三個階段：建構、實例化、確定/決定來試著以非同步形式來執行

其中建構步驟會是向第三方索要對應模組檔案並建立module graph來表示每個模組之間的依賴關係。

> build up their understanding of the module graph before getting down to the synchronous work of instantiating.

實例化對於同個模組的載入任務來說，會是依賴著建構任務完成才會做的任務，但是對於不同模組來說，卻可以是以非同步來完成


> This approach—having the algorithm split up into phases—is one of the key differences between ES modules and CommonJS modules.

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

> But sometimes it is really useful to use variables for module paths. For example, you might want to switch which module you load depending on what the code is doing or what environment it is running in.

> To make this possible for ES modules, there’s a proposal called [dynamic import](https://github.com/tc39/proposal-dynamic-import). With it, you can use an import statement like ``import(`${path}/foo.js`)``.

> The way this works is that any file loaded using `import()` is handled as the entry point to a separate graph. The dynamically imported module starts a new graph, which is processed separately.

如果要根據執行狀態下載入ES module的話，可以使用dynamic import來實現，該技術會以產出非同步任務為主的promise為主，

具體使用方式：import 為promise，當呼叫時會對系統發出以module1的載入請求，處理期間會另外建立以module1為主的模組依賴關係圖(graph)，並建立實例、執行對應的top-level code來更新實例下的內容，接著當處理成功時並能回傳實例或者處理失敗時，就會分別回傳resolve或者reject。
```
import(module_path/module1)
```


[![Two module graphs with a dependency between them, labeled with a dynamic import statement](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/14dynamic_import_graph-500x389.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/14dynamic_import_graph.png)

> One thing to note, though — any module that is in both of these graphs is going to share a module instance. This is because the loader caches module instances. For each module in a particular global scope, there will only be one module instance.

> This means less work for the engine. For example, it means that the module file will only be fetched once even if multiple modules depend on it. (That’s one reason to cache modules. We’ll see another in the evaluation section.)

> The loader manages this cache using something called a [module map](https://html.spec.whatwg.org/multipage/webappapis.html#module-map). Each global keeps track of its modules in a separate module map.

> When the loader goes to fetch a URL, it puts that URL in the module map and makes a note that it’s currently fetching the file. Then it will send out the request and move on to start fetching the next file.



[![The loader figure filling in a Module Map chart, with the URL of the main module on the left and the word fetching being filled in on the right](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/15_module_map-500x170.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/15_module_map.png)

> What happens if another module depends on the same file? The loader will look up each URL in the module map. If it sees `fetching` in there, it will just move on to the next URL.


系統要開始載入模組A而先從網路獲取模組檔案A時，會從Module Map檢查看看是否存在模組檔案A所在URL，若沒有的話，就設定對應的URL來表示模組A，並填入狀態為fetching，來表示該模組A正在被獲取中；反之，若有的話，就改處理另一個模組的載入

接著其他模組想要載入模組A的話，就會先從Module Map檢查看看是否存放模組A所在的URL，在這裡是有，所以其他模組會改處理另一批模組的載入工作。

> But the module map doesn’t just keep track of what files are being fetched. The module map also serves as a cache for the modules, as we’ll see next.

module map 主要的用途為：
- 顯示每個正在被載入的模組之狀態
- 藉由狀態來避免重複實例、重複執行/確定、重複下載
- 若有被實例化，狀態會含有對應模組實例在記憶體中的位置，以此作為緩存實例的作用

### 本地端存取速率 vs 網路速率
在最糟糕的情況下，是可以把兩者的速率想成非常糟糕，然而本地端存取比起網路來得好解決，因為我們只需要更替更好的本地端設備就能直接解決，然而網路卻沒辦法好解決更替網路設備就能直接性解決速率問題，還得考慮網路節點間的傳遞問題，而這些節點卻是另一些主機來管理，這些主機往往都無法直接性調整


### 為何避免多個不同模組索要相同模組而做的重複性索要
N個模組索要模組代表有N個任務會同時想要獲取模組，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時索取模組，但若模組是相同的話，將會有N個相同模組，然而，實際上也只需要一個，所以這對於瀏覽器來說，由於多做載入而使效能衰減

#### 如何避免多個不同模組索要相同模組而做的重複性索要？
使用module map＋鎖的機制，讓只有一個任務能夠負責特定模組檔案的索要，並在module map以模組所在的URL作為索引來標記fetching來告知其他任務每次做之前都會從module map檢查要找的模組是否還有沒有人找：
	- 若對應模組狀態顯示fetching，任務就找下一個想要載入的模組
	- 若找不到，任務就當那個第一個要載入特定模組的任務，剩下要做相同內容的任務就停留在要讀取map的時候，第一個任務做完載入並標記fetching，最後解鎖讓其他任務去檢查

## 複習

#🧠 ES module： 在建構階段中，會做哪些事情->->-> `替每個模組解析模組在哪個主機可以載入、從對應主機載入對應模組、將每個對應模組解析成module record、根據import/export以圖狀資料結構來產生模組依賴關係圖`

#🧠 ES module：module specifier 具體是什麼？ ->->-> `是指定module是源自於哪裡的module，具體可以搭配URL、本地端的相對路徑和絕對路徑`

#🧠 ES module：module specifier 在建構上會做什麼解析？ 每個平台都一樣？->->-> `系統會以自己平台上所支援的解析方式來解析specifier，並了解對應模組哪裡`

#🧠 ES module：為了解決每個平台對於module specifier的解析不同，而提出什麼 ->->-> `為了統一各平台對於module specifier的解析，有人就提出module resolution algorithm，能根據平台來以不同的方式解析`

#🧠 ES module：以圖中例子來說說明模組的建構階段 ![A diagram that shows one file being fetched and then parsed, and then two more files being fetched and then parsed](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/10_construction-500x302.png) ->->-> `瀏覽器會使用URL作為module specifier，模組的依賴關係會從從對應主機獲取(fetch)對應main.js模組，然後解析成對應module record來找到main.js模組依賴的模組是哪些，然後再從模組的module specifier找對對應主機獲取(fetch)對應依賴模組，接著在解析成對應module record，找到是否有依賴模組。`


#🧠 ES module：瀏覽器的模組源自於哪裡？ ->->-> `網路、本地端的儲存設備`

#🧠 ES module：在最糟的情況下，瀏覽器建構在網路上的模組和本地端上的模組下，都由什麼來決定效能？ ->->-> `瀏覽器的模組源自於以下兩個地方，且效率會侷限於網路和存取設備，一般來說，網路速率會比存取設備還慢：1.  第三方模組：網路上下載至本地端速率＋從本地端載入檔案至專案的速率 2.  本地端模組：從本地端載入檔案至專案的速率`


#🧠 ES module：主要在什麼時候會載入其模組內容至需求方->->-> `ES 模組 本身是在主程式和模組這兩者的編譯/解析期間就載入模組內容至需求方`

#🧠 ES module：能否依據執行情況來載入特定模組，不考慮動態載入的話 ->->-> `不能，因為已經在編譯期間完成載入。`

#🧠 ES module：不能依據執行情況來載入特定模組，有辦法可以解決嗎->->-> `有，如果要根據執行狀態下載入ES module的話，可以使用dynamic import來實現，該技術會以產出非同步任務為主的promise為主`

#🧠 ES module：具體的dynamic import是什麼？ ->->-> `import 為promise，當呼叫時會對系統發出以module1的載入請求，處理期間會另外建立以module1為主的模組依賴關係圖(graph)，並建立實例、執行對應的top-level code來更新實例下的內容，接著當處理成功時並能回傳實例或者處理失敗時，就會分別回傳resolve或者reject`

#🧠  ES module：具體的dynamic import形式會是什麼？ ->->-> `import(module_path/module1)`


#🧠 ES module：module map會用做什麼？ ->->-> `- 顯示每個正在被載入的模組之狀態 - 藉由狀態來避免重複實例、重複執行/確定、重複下載 - 若有被實例化，狀態會含有對應模組實例在記憶體中的位置，以此作為緩存實例的作用`

#🧠 對於本地端存取和網路速率來說，最糟糕的速率會是如何以及如何解決？ ->->-> `在最糟糕的情況下，是可以把兩者的速率想成非常糟糕，然而本地端存取比起網路來得好解決，因為我們只需要更替更好的本地端設備就能直接解決，然而網路卻沒辦法好解決更替網路設備就能直接性解決速率問題，還得考慮網路節點間的傳遞問題，而這些節點卻是另一些主機來管理，這些主機往往都無法直接性調整`

#🧠 ES module：為何要避免多個不同模組索要相同模組而做的重複性索要->->-> `多個模組索要模組代表有N個任務會同時想要獲取模組，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時索取模組，但若模組是相同的話，將會有N個相同模組，然而，實際上也只需要一個，所以這對於瀏覽器來說，由於多做載入而使效能衰減`


#🧠 ES module：如何避免多個不同模組索要相同模組而做的重複性索要？ ->->-> `使用module map＋鎖的機制，讓只有一個任務能夠負責特定模組檔案的索要，並在module map以模組所在的URL作為索引來標記fetching來告知其他任務每次做之前都會從module map檢查要找的模組是否還有沒有人找： - 若對應模組狀態顯示fetching，任務就找下一個想要載入的模組 - 若找不到，任務就當那個第一個要載入特定模組的任務，剩下要做相同內容的任務就停留在要讀取map的時候，第一個任務做完載入並標記fetching，最後解鎖讓其他任務去檢查`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive(3) - Parsing 筆記]]
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
[[es-modules-a-cartoon-deep-dive(4) - Instantiation 筆記]]
[[es-modules-a-cartoon-deep-dive(5) - Evaluation 筆記]]
[[es-modules-a-cartoon-deep-dive  - module map]]
References:
[[@htmlspecHTMLStandard]]
[[@wikidataEvaluationDisambiguation2022]]