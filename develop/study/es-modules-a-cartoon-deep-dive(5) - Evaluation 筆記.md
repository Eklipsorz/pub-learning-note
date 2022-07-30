## 描述


#### Evaluation

> The final step is filling in these boxes in memory. The JS engine does this by executing the top-level code — the code that is outside of functions.
> 
> Besides just filling in these boxes in memory, evaluating the code can also trigger side effects. For example, a module might make a call to a server.



[![A module will code outside of functions, labeled top level code](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/40_top_level_code-500x146.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/40_top_level_code.png)

> Because of the potential for side effects, you only want to evaluate the module once. As opposed to the linking that happens in instantiation, which can be done multiple times with exactly the same result, evaluation can have different results depending on how many times you do it.

> This is one reason to have the module map. The module map caches the module by canonical URL so that there is only one module record for each module. That ensures each module is only executed once. Just as with instantiation, this is done as a depth first post-order traversal.

最後一步：透過執行模組來將實際值分配至識別字對應的記憶體空間，流程是當第一個需求方(需要該模組的模組)已經替模組實例化時，就會執行evaluation這步驟，但為了確保後續多個需求方可能由於依賴關係圖而重複實例化＋evaluation，會藉由module map來讓多個需求方的情況下，每個需求方只會拿到對應模組的同一個實例，具體是：當第一個需求方(需要該模組的模組)已經替模組實例化時，還有其他需求方索要同一個模組時
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

## 複習

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
References:
[[@linclarkESModulesCartoon]]