## 描述


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


### 

> 评估主要由函数InnerModuleEvaluation实现。函数 InnerModuleEvaluation 会调用函数ExecuteModule，该函数会评估模块代码（evaluating module.[[ECMAScriptCode]]）。ES6 规范并没有明确说明这里的评估模块代码具体指什么。我把 ES6 规范的相关部分反复看了至少十余遍，才得出一个比较合理的解释。这里的评估模块代码应该指根据代码语句顺序执行条款 13、条款 14和条款 15内的对应小节的“运行时语义：评估（Runtime Semantics: Evaluation）”。ScriptEvaluation中的评估脚本（evaluating scriptBody）应该也是这个意思。可以看到，ES6 规范虽然做了很多设计并且逻辑清晰和自洽，但仍有一些模棱两可的地方，没有达到一种绝对完善和无懈可击的状态。

> 对于图 3 的模块关系，评估过程如图 8 所示。和连接阶段类似，评估阶段也采用深度优先遍历，通过函数 HostResolveImportedModule 获取子模块。完成核心操作的函数 ExecuteModule 是后置执行的，所以从效果上看，子模块先于父模块被执行。


![](https://pic4.zhimg.com/80/v2-70b40b2e27f95a761e620c077aad7c7f_720w.jpg)
图 8

> 由于连接阶段会给导入模块变量创建绑定并初始化为子模块的对应变量，子模块的对应变量在评估阶段会先被赋值，所以导入模块变量获得了和函数声明变量一样的提升效果。例如，代码 1 是能正常运行的。因此，ES6 模块的导入导出语句的位置不影响模块代码语句的执行结果。
### cyclic dependency detect & solve
[[環狀依賴結構會是指多個模組因為彼此依賴而在依賴關係上構成多個模組構成的環狀依賴結構]]

若以ES Module的實例化＋evaluation來說的話：
- 不斷繞著環狀結構遍歷，直到超過時間，超過時間就結束環狀遍歷
- 停止的時候，環狀結構的每個模組都指向到識別字對應的記憶體區塊
## 複習

#🧠 ES module：evaluation 是什麼？ ->->-> `透過執行模組的top-level code來將實際值分配至識別字對應的記憶體空間`

#🧠  ES module：如何解決以模組角度來解決cyclic dependency ？ ->->-> `不斷繞著環狀結構遍歷，直到超過時間，超過時間就結束環狀遍歷，停止的時候，環狀結構的每個模組都指向到識別字對應的記憶體區塊`

#🧠 ES Module：當有多個模組想要對同一個模組進行實例化＋evaluation的話，請問會如何解決？ ->->-> `只允許一個模組做實例化+evaluation，第一個需求方(需要該模組的模組)已經替模組實例化時，就會執行evaluation這步驟，但為了確保後續多個需求方可能由於依賴關係圖而重複實例化＋evaluation，會藉由module map來讓多個需求方的情況下，每個需求方只會拿到對應模組的同一個實例，具體是：當第一個需求方(需要該模組的模組)已經替模組實例化＋evaluation時，還有其他需求方索要同一個模組時 - 先透過模組(URL)來查看其模組在module map的狀態 - 若狀態是module record，就從module record獲取對應模組實例的module environment record，該record會告知對應實例所要輸出的內容之記憶體位置`

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