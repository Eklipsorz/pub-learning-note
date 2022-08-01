## 描述



### 文獻1說明

#### Evaluation

> The final step is filling in these boxes in memory. The JS engine does this by executing the top-level code — the code that is outside of functions.
> 
> Besides just filling in these boxes in memory, evaluating the code can also trigger side effects. For example, a module might make a call to a server.


[![A module will code outside of functions, labeled top level code](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/40_top_level_code-500x146.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/40_top_level_code.png)

> Because of the potential for side effects, you only want to evaluate the module once. As opposed to the linking that happens in instantiation, which can be done multiple times with exactly the same result, evaluation can have different results depending on how many times you do it.

> This is one reason to have the module map. The module map caches the module by canonical URL so that there is only one module record for each module. That ensures each module is only executed once. Just as with instantiation, this is done as a depth first post-order traversal.

最後一步：透過執行模組的top-level code來將實際值分配至識別字對應的記憶體空間，流程是當第一個需求方(需要該模組的模組)已經替模組實例化時，就會執行evaluation這步驟，但為了確保後續多個需求方可能由於依賴關係圖而重複實例化＋evaluation，會藉由module map來讓多個需求方的情況下，每個需求方只會拿到對應模組的同一個實例，具體是：當第一個需求方(需要該模組的模組)已經替模組實例化時，還有其他需求方索要同一個模組時
- 先透過模組(URL)來查看其模組在module map的狀態
- 若狀態是module record，就從module record獲取對應模組實例的module environment record，該record會告知對應實例所要輸出的內容之記憶體位置



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

> If the export were handled using live bindings, the counter module would see the correct value eventually. By the time the timeout runs, `main.js`’s evaluation would have completed and filled in the value.

> Supporting these cycles is a big rationale behind the design of ES modules. It’s this three-phase design that makes them possible.


### 文獻2說明
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]] 

> 评估主要由函数InnerModuleEvaluation实现。函数 InnerModuleEvaluation 会调用函数ExecuteModule，该函数会评估模块代码（evaluating module.[[ECMAScriptCode]]）。ES6 规范并没有明确说明这里的评估模块代码具体指什么。我把 ES6 规范的相关部分反复看了至少十余遍，才得出一个比较合理的解释。这里的评估模块代码应该指根据代码语句顺序执行条款 13、条款 14和条款 15内的对应小节的“运行时语义：评估（Runtime Semantics: Evaluation）”。ScriptEvaluation中的评估脚本（evaluating scriptBody）应该也是这个意思。可以看到，ES6 规范虽然做了很多设计并且逻辑清晰和自洽，但仍有一些模棱两可的地方，没有达到一种绝对完善和无懈可击的状态。

> 对于图 3 的模块关系，评估过程如图 8 所示。和连接阶段类似，评估阶段也采用深度优先遍历，通过函数 HostResolveImportedModule 获取子模块。完成核心操作的函数 ExecuteModule 是后置执行的，所以从效果上看，子模块先于父模块被执行。


![](https://pic4.zhimg.com/80/v2-70b40b2e27f95a761e620c077aad7c7f_720w.jpg)
图 8

> 由于连接阶段会给导入模块变量创建绑定并初始化为子模块的对应变量，子模块的对应变量在评估阶段会先被赋值，所以导入模块变量获得了和函数声明变量一样的提升效果。例如，代码 1 是能正常运行的。因此，ES6 模块的导入导出语句的位置不影响模块代码语句的执行结果。

[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]] 
> ECMAScript 6 入门教程》一书说的三个重大差异如下：
> 1.  CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。  
> 2.  CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。  
> 3.  CommonJS 模块的`require()`是同步加载模块，ES6 模块的`import`命令是异步加载，有一个独立的模块依赖的解析阶段。  
    
> 对于第 1 点，CommonJS 和 ES6 模块输出的都是变量，变量都是值的引用。该章节的评论中也有人质疑这个点。
> 
> 对于第 2 点，前半句基本正确，后半句基本错误。CommonJS 模块在执行阶段加载子模块文件，ES6 模块在预处理阶段加载子模块文件，当然 ES6 模块在执行阶段也会加载子模块文件，不过会使用预处理阶段的缓存。从形式上看，CommonJS 模块整体导出一个包含若干个变量的对象，ES6 模块分开导出单个变量，如果只看父模块，ES6 模块的父模块确实在预处理阶段就绑定了子模块的导出变量，但是预处理阶段的子模块的导出变量是还没有被赋最终值的，所以并不能算真正输出。
> 
> 对于第 3 点，CommonJS 模块同步加载并执行模块文件，ES6 模块提前加载并执行模块文件。异步通常被理解为延后一个时间节点执行，所以说成异步加载是错误的。

重點：
- 到此階段的模組，一開始的模組紀錄狀態皆為linked
- 每一次挑選模組會透過模組依賴關係圖來找出模組要來做evaluation：
	- 模組會是沒依賴任何模組的模組
	- 模組會是依賴著已經完成evaluation的模組的模組
- evaluation會做：
	- 更新module map上的對應模組紀錄狀態：從linked變更至evaluating
	- 執行時透過import來在執行時期加載該模組所依賴的模組，具體會透過模組所在的主機來在module map找到對應的module record，接著再從裡頭找到environment record來讓import識別字對應至正確的記憶體位置
	- 透過執行模組的top-level code來將實際值分配至export那邊識別字對應的記憶體空間
	- 更新module map上的對應模組紀錄狀態：從evaluating 變更至 evaluated



### N個不同模組會替相同模組做N個同個實例的執行？

N個模組要求模組做evaluation代表有N個任務會同時要求模組做evaluation，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時要求模組做evaluation，但若模組是相同的話，將會有N個相同模組下的evaluation，然而，實際上也只需要執行一次evaluation，所以這對於瀏覽器來說，是種浪費，也是一種效能改善的方向

#### 如何避免N個不同模組會替相同模組做N個同個實例的執行？

使用module map＋上鎖/解鎖的機制，每一個首次要求做對應模組實例的任務會先對module map對應模組紀錄進行上鎖，並檢查以下條件是否滿足：
- module map的對應模組紀錄狀態上是顯示linked?
若任一條件滿足就做：
	- 更新module map上的對應模組紀錄狀態：從linked變更至evaluating
	- 替module map上的對應模組紀錄進行解鎖
	- 執行時透過import來在執行時期加載該模組所依賴的模組，具體會透過模組所在的主機來在module map找到對應的module record，接著再從裡頭找到environment record來讓import識別字對應至正確的記憶體位置
	- 透過執行模組的top-level code來將實際值分配至export那邊識別字對應的記憶體空間
	- 更新module map上的對應模組紀錄狀態：從evaluating 變更至 evaluated

若都不滿足，就解鎖然後挑下一個要執行evaluation的模組。


### cyclic dependency detect & solve
[[環狀依賴結構會是指多個模組因為彼此依賴而在依賴關係上構成多個模組構成的環狀依賴結構]]

若以ES Module的實例化＋evaluation來說的話：
- 不斷繞著環狀結構遍歷，直到超過時間，超過時間就結束環狀遍歷
- 停止的時候，環狀結構的每個模組都指向到識別字對應的記憶體區塊
## 複習

#🧠 ES module：evaluation 是什麼？ ->->-> `透過執行模組的top-level code來將實際值分配至識別字對應的記憶體空間`

#🧠 ES Module：請問evaluation階段需要等待全部模組都完成instantiation階段？為何 ->->-> `對，這是因爲要確保生成的非同步任務都是在處理evaluation、解決模組依賴關係`

#🧠 ES Module：會重新在挑模組來執行evaluation嗎？是的話，如何挑 ->->-> `要重新挑，這是為了確保exporting module都能確實使用它所依賴的模組來輸出內容至importing module，至於如何挑，會以DFS post-order traversal來從模組依賴關係圖來優先從底部挑選模組會是沒依賴任何模組的模組、 模組會是依賴著已經完成evaluation的模組的模組`


#🧠 ES Module：當有多個模組想要對同一個模組進行實例化＋evaluation的話，請問會如何解決？ ->->-> `只允許一個模組做實例化+evaluation，第一個需求方(需要該模組的模組)已經替模組實例化時，就會執行evaluation這步驟，但為了確保後續多個需求方可能由於依賴關係圖而重複實例化＋evaluation，會藉由module map來讓多個需求方的情況下，每個需求方只會拿到對應模組的同一個實例，具體是：當第一個需求方(需要該模組的模組)已經替模組實例化＋evaluation時，還有其他需求方索要同一個模組時 - 先透過模組(URL)來查看其模組在module map的狀態 - 若狀態是module record，就從module record獲取對應模組實例的module environment record，該record會告知對應實例所要輸出的內容之記憶體位置`

#🧠 ES Module：經過實例後的模組紀錄，在一開始進入evaluation時會拿到什麼狀態？ ->->-> `linked`

#🧠 ES Module：每一個被挑到執行evaluation的模組如何實作evaluation？ ->->-> `	- 更新module map上的對應模組紀錄狀態：從linked變更至evaluating - 執行時透過import來在執行時期加載該模組所依賴的模組，具體會透過模組所在的主機來在module map找到對應的module record，接著再從裡頭找到environment record來讓import識別字對應至正確的記憶體位置 - 透過執行模組的top-level code來將實際值分配至export那邊識別字對應的記憶體空間 - 更新module map上的對應模組紀錄狀態：從evaluating 變更至 evaluated`


#🧠 ES Module：N個不同模組會替相同模組做N個同個實例的執行？ ->->-> `N個模組要求模組做evaluation代表有N個任務會同時要求模組做evaluation，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時要求模組做evaluation，但若模組是相同的話，將會有N個相同模組下的evaluation，然而，實際上也只需要執行一次evaluation，所以這對於瀏覽器來說，是種浪費，也是一種效能改善的方向`

#🧠 ES Module：如何避免N個不同模組會替相同模組做N個同個實例的執行？ 假如使用使用module map＋上鎖/解鎖的機制，那麼上鎖條件/解鎖條件會是？->->-> `每一個首次要求做對應模組實例的任務會先對module map對應模組紀錄進行上鎖，並檢查以下條件是否滿足：- module map的對應模組紀錄狀態上是顯示linked?，若不滿足，就解鎖然後挑下一個要執行evaluation的模組；若滿足，就- 更新module map上的對應模組紀錄狀態：從linked變更至evaluating- 替module map上的對應模組紀錄進行解鎖`

#🧠 ES Module：如何避免N個不同模組會替相同模組做N個同個實例的執行？ 假如使用使用module map＋上鎖/解鎖的機制，那麼得滿足什麼樣條件才能做evaluation? ->->-> `module map的對應模組紀錄狀態上是顯示linked?`

#🧠 ES Module：如何避免N個不同模組會替相同模組做N個同個實例的執行？ 假如使用使用module map＋上鎖/解鎖的機制，會設定條件且滿足條件的話，具體會如何做evaluation?  ->->-> `	- 更新module map上的對應模組紀錄狀態：從linked變更至evaluating - 替module map上的對應模組紀錄進行解鎖 - 執行時透過import來在執行時期加載該模組所依賴的模組，具體會透過模組所在的主機來在module map找到對應的module record，接著再從裡頭找到environment record來讓import識別字對應至正確的記憶體位置 - 透過執行模組的top-level code來將實際值分配至export那邊識別字對應的記憶體空間 - 更新module map上的對應模組紀錄狀態：從evaluating 變更至 evaluated`


---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
[[es-modules-a-cartoon-deep-dive(3) - Parsing 筆記]]
[[es-modules-a-cartoon-deep-dive  - 用語介紹]]
[[es-modules-a-cartoon-deep-dive(4) - Instantiation 筆記]]
[[環狀依賴結構會是指多個模組因為彼此依賴而在依賴關係上構成多個模組構成的環狀依賴結構]]
References:
[[@linclarkESModulesCartoon]]
[[@DetectCycleDirected2012]]
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]