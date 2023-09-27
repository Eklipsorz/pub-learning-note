## 描述

### 文獻1的說明
[[@linclarkESModulesCartoon]]



> Like I mentioned before, an instance combines code with state. That state lives in memory, so the instantiation step is all about wiring things up to memory.

JS 引擎當做完實例化後，會替每一個模組實例建立一個module environment record來管理模組實例所使用到的識別字和對應識別字的實體物件，並讓(位處於module map之對應模組欄位)**module record 的屬性environment去指向module environment record**

> First, the JS engine creates a module environment record. This manages the variables for the module record. Then it finds boxes in memory for all of the exports. The module environment record will keep track of which box in memory is associated with each export.


分配記憶體區塊給模組所要輸出的內容，在實例化的階段，只會賦予初始值，並不會按照模組的code來賦予實際值。

> These boxes in memory won’t get their values yet. It’s only after evaluation that their actual values will be filled in. There is one caveat to this rule: any exported function declarations are initialized during this phase. This makes things easier for evaluation.

> To instantiate the module graph, the engine will do what’s called a depth first post-order traversal. This means it will go down to the bottom of the graph — to the dependencies at 
> the bottom that don’t depend on anything else — and set up their exports.

實例化會先從模組依賴關係圖的底部開始實例化，底部的模組都完成實例化，就往上一層的模組進行實例化，後面以此類推。


> The engine finishes wiring up all of the exports below a module — all of the exports that the module depends on. Then it comes back up a level to wire up the imports from that module.

> Note that both the export and the import point to the same location in memory. Wiring up the exports first guarantees that all of the imports can be connected to matching exports.


![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_01-768x316.png)

> The engine finishes wiring up all of the exports below a module — all of the exports that the module depends on. Then it comes back up a level to wire up the imports from that module.

> Note that both the export and the import point to the same location in memory. Wiring up the exports first guarantees that all of the imports can be connected to matching exports.


在實例化的過程中，會讓所有export所指定的識別字與記憶體區塊做一個對應關係，同時間也會讓import的識別字所對應的記憶體區塊也和export所對應的一樣，確保兩者都能使用相同的記憶體區塊



![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_02-768x316.png)

> This is different from CommonJS modules. In CommonJS, the entire export object is copied on export. This means that any values (like numbers) that are exported are copies.

> This means that if the exporting module changes that value later, the importing module doesn’t see that change.

commonJS 模組A的實例化也是存放在記憶體，當需求方想要載入commonJS 模組A時，就複製存放記憶體內的實例並將副本放置另一個記憶體區塊任由需求方去存取，這時會有兩個記憶體分別存放著commonJS模組A和commonJS模組A副本

![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)

> In contrast, ES modules use something called live bindings. Both modules point to the same location in memory. This means that when the exporting module changes a value, that change will show up in the importing module.

live bindings：概念上會是exporting module輸出的識別字和importing module引用的識別字都各自指向相同的記憶體區塊，當exporting module改變識別字對應的記憶體區塊內容，importing module就會馬上看到其識別字對應的(記憶體區塊)內容

> Modules that export values can change those values at any time, but importing modules cannot change the values of their imports. That being said, if a module imports an object, it can change property values that are on that object.


實例化：
1. 先透過Depth First Post-Order Travesal來從模組依賴關係圖的起始點轉移至圖的底部，該底部的模組會是沒有使用任何依賴或者使用著已經完成實例化模組的模組，試圖先實例化沒有任何依賴的模組群組A，接著實例化依賴著模組群組A的模組群組B，然後一直往上實例，直到遍歷完所有模組並做完所有模組的實例
2. 每一次實例會按照順序做以下事情：
	- 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；替輸出var變數宣告分配一塊記憶體，初始值為undefined
	- 建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件
	- 藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record**
	- 替當前的模組處理 export 和 import：將export的識別字和import的識別字分別指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊

3. 限制：相對來說，ES 模組會使用live bindings技術來讓模組間的export和import所指的識別字都指向同個記憶體區塊，這表示只要在模組上更改值，就會使用import的那一方拿到變更後的值，但只有exporting module那一方才能更改對應的值，importing module不能夠更改import識別字上的對應實體物件(記憶體內容)，最多只能增加屬性至物件上。

![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_04-768x316.png)

> The reason to have live bindings like this is then you can wire up all of the modules without running any code. This helps with evaluation when you have cyclic dependencies, as I’ll explain below.

### 文獻2的說明
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]

![](https://pic2.zhimg.com/80/v2-72974a333dc76a845ef3aed4d9aa9dc5_720w.jpg)
图 3

> 模块执行顺序

> ES6 模块有 5 种状态，分别为 unlinked、linking、linked、evaluating 和 evaluated，用循环模块记录（Module Environment Records）的 Status 字段表示。ES6 模块的处理包括连接（link）和评估（evaluate）两步。连接成功之后才能进行评估。

> 连接主要由函数InnerModuleLinking实现。函数 InnerModuleLinking 会调用函数InitializeEnvironment，该函数会初始化模块的环境记录（Environment Records），主要包括创建模块的执行上下文（Execution Contexts）、给导入模块变量创建绑定并初始化为子模块的对应变量，给 var 变量创建绑定并初始化为 undefined、给函数声明变量创建绑定并初始化为函数体的实例化值、给其他变量创建绑定但不进行初始化。

> 对于图 3 的模块关系，连接过程如图 7 所示。连接阶段采用深度优先遍历，通过函数HostResolveImportedModule获取子模块。完成核心操作的函数 InitializeEnvironment 是后置执行的，所以从效果上看，子模块先于父模块被初始化。

![](https://pic1.zhimg.com/80/v2-30e4837c0538d925a507debd89af3180_720w.jpg)
图 7




重點：
- ES 模組各有5種狀態會紀錄每個模組的目前載入狀況，並記錄在module record：
	- unlinked：未被進行模組上初始化和識別字連接
	- linking：正在進行模組上的初始化和識別字連接
	- linked：已完成模組上的初始化和識別字連接
	- evaluating：已完成實例化這步驟，並正在執行對應模組的top-level code
	- evaluated：已完成實例化這部分，且也完成了對應模組上top-level code的執行
- 到此階段的模組，一開始的模組紀錄狀態皆為unlinked
- 每一次挑選模組會透過模組依賴關係圖來找出模組要來做實例化：
	- 模組會是沒依賴任何模組的模組
	- 模組會是依賴著已經完成實例化的模組的模組
- 實例化會做：
	- 更改對應module record上的狀態：unlinked -> linking
	- 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；替輸出var變數宣告分配一塊記憶體，初始值為undefined
	- 建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件
	- 藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record**
	- 替當前的模組處理 export 和 import：將export的識別字和import的識別字分別指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊
	- 更改對應module record的狀態：linking->linked

- 注意細節：
	- 做完實例化並不會直接做evaluation，會等全部模組的instantiation 的做完才會做evaluation

### N個不同模組會替相同模組做N個重複性實例化？

N個模組要求模組做實例化代表有N個任務會同時要求模組做實例化，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時要求模組實例化，但若模組是相同的話，將會有N個相同模組下的實例，然而，實際上也只需要一個實例，所以這對於瀏覽器來說，是種浪費，也是一種效能改善的方向

#### 如何避免N個不同模組會替相同模組做N個重複性實例化？


使用module map＋上鎖/解鎖的機制，每一個首次要求做對應模組實例的任務會先對module map對應模組紀錄進行上鎖，並檢查以下條件是否滿足：
- module map的對應模組紀錄沒對應到environment record？
- module map的對應模組紀錄是unlinked?
若任一條件滿足就做：
- 將module map的對應模組紀錄狀態更改：unlinked -> linking
- 對module map的對應模組紀錄上解鎖
- 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；替輸出var變數宣告分配一塊記憶體，初始值為undefined
- 替對應模組建立environment record
-  藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record**
- 替當前的模組處理 export 和 import：將export的識別字和import的識別字分別指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊
- 將module map的對應模組紀錄狀態更改：linking -> linked

若都不滿足，就解鎖然後就挑下一個要實例化的模組。



### importing module 在live bindings下可以更改exporting的物件

module1.mjs
```
export let testvar1 = {};
```

module2.mjs
```
import { testvar1 } from './module1.mjs';

testvar1.test1 = 'test1'
testvar1.test2 = 'test1';
console.log(testvar1)

delete testvar1.test1
console.log(testvar1)
```

```
{ test1: 'test1', test2: 'test1' }
{ test2: 'test1' }
```

重點：
- 原本是一旦live bindings建立後，importing module就不能修改exporting module所輸出的內容
- 若內容會是物件的話，則可以透過參照關係來修改物件本身的內容，由於真正禁止不能修改的記憶體區塊是在stack記憶體區塊

## 複習
#🧠 ES Module：請問instantiation階段需要等待全部模組都完成construction階段？為何 ->->-> `對，這是要為了確保多個非同步任務在同時執行的過程只會侷限於instantiation 階段，避免有不一致的問題`
<!--SR:!2023-09-27,3,250-->


#🧠 ES 模組各有5種狀態會紀錄每個模組的目前載入狀況，並記錄在module record，請問是哪五種狀態？具體做什麼？ ->->-> `	- unlinked：未被進行模組上初始化和識別字連接 - linking：正在進行模組上的初始化和識別字連接 - linked：已完成模組上的初始化和識別字連接 - evaluating：已完成實例化這步驟，並正在執行對應模組的top-level code - evaluated：已完成實例化這部分，且也完成了對應模組上top-level code的執行`
<!--SR:!2023-09-27,3,250-->

#🧠 ES Module：經過建構後的模組紀錄，在一開始進入實例化前會拿到什麼狀態？ ->->-> `unlinked`
<!--SR:!2024-11-12,504,250-->


#🧠 ES Module： 每一個模組的實例會如何做？(提示：有六個步驟)->->-> `	- 更改對應module record上的狀態：unlinked -> linking - 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；替輸出var變數宣告分配一塊記憶體，初始值為undefined - 建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件 - 藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record** - 替當前的模組處理 export 和 import：將export的識別字和import的識別字分別指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊 - 更改對應module record的狀態：linking->linked`
<!--SR:!2023-09-27,3,250-->


#🧠 ES Module：從模組依賴關係圖要找到什麼才開始實例化->->-> `沒使用任何依賴或者使用著已經完成實例化模組的模組`
<!--SR:!2024-04-10,374,250-->

#🧠 ES Module：從模組依賴關係圖要找到沒使用任何依賴或者使用著已經完成實例化模組的模組，那麼如何找？ ->->-> `模組依賴關係圖底部或者越往底部正是那些，所以會使用Depth First Post-Order Travesal來從模組依賴關係圖的起始點轉移至圖的底部，試圖先實例化沒有任何依賴的模組群組A，接著實例化依賴著模組群組A的模組群組B，然後一直往上實例，直到遍歷完所有模組並做完所有模組的實例`
<!--SR:!2024-04-07,371,250-->


#🧠 用這兩張圖來說明ES module 的實例化，其中右邊是main.js，左邊由先至後是counter.js和render.js，主要main.js會依賴這兩個模組![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_01-768x316.png) ![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_02-768x316.png)->->-> ``
<!--SR:!2024-02-03,337,250-->

#🧠 ES module的live bindings是什麼？ ->->-> `概念上會是exporting module輸出的識別字和importing module引用的識別字都各自指向相同的記憶體區塊，當exporting module改變識別字對應的記憶體區塊內容，importing module就會馬上看到其識別字對應的(記憶體區塊)內容`
<!--SR:!2023-10-08,10,250-->

`

#🧠 ES module：一旦建立live bindings，會有哪些限制 ->->-> `相對來說，ES 模組會使用live bindings技術來讓模組間的export和import所指的識別字都指向同個記憶體區塊，這表示只要在模組上更改值，就會使用import的那一方拿到變更後的值，但只有exporting module那一方才能更改對應的值，importing module不能夠更改import識別字上的對應實體物件(記憶體內容)，最多只能增加屬性至物件上。`
<!--SR:!2023-09-27,3,250-->



#🧠 ES module：一旦建立live bindings，原本是一旦live bindings建立後，importing module就不能修改exporting module所輸出的內容， importing module部分若存取到物件的話，可以修改物件的屬性嗎？ ->->-> `可以像存取到物件那樣去修改物件本身的屬性`
<!--SR:!2024-02-06,287,247-->


#🧠 ES module：以下是建立live bindings，請問module2.mjs最後會印出什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666158493/blog/es-module/live-bindings-example_dxe2qu.png) ->->-> `{ test1: 'test1', test2: 'test1' } { test2: 'test1' }`
<!--SR:!2023-11-06,230,247-->

#🧠 ES Module：  N個不同模組會是替相同模組做N個重複性實例化？請說明可能性 ->->-> `通常會以模組依賴關係圖來找模組，依賴關係圖中會有被依賴的模組A和依賴模組A的模組B，當出現時，系統會為了方便實例化兩個模組，會先從被依賴的模組A開始實例化，換言之就是會產生任務去對模組A做實例化，若有N個模組要同樣的模組A，即為發送N個任務來對模組A做實例化，將會有N個相同模組下的實例，然而，實際上也只需要一個實例，所以這對於瀏覽器來說，是種浪費，也是一種效能改善的方向`
<!--SR:!2023-09-27,3,250-->



#🧠 ES Module：如何避免N個不同模組會替相同模組做N個重複性實例化？假設使用module map＋上鎖/解鎖的機制，那要如何設定上鎖條件/解鎖條件？ ->->-> `每一個首次要求做對應模組實例的任務會先對module map對應模組進行上鎖，並檢查以下條件是否滿足： - module map的對應模組紀錄沒對應到environment record？ - module map的對應模組紀錄是unlinked? 若滿足的話，就將module map的對應模組紀錄狀態更改：unlinked -> linking，接著解鎖；反之若不滿足的話，就解鎖然後就挑下一個要實例化的模組`
<!--SR:!2023-09-27,3,250-->


#🧠 ES Module：如何避免N個不同模組會替相同模組做N個重複性實例化？假設使用module map＋上鎖/解鎖的機制，每一個首次要求做對應模組實例的任務會先對module map對應模組紀錄進行上鎖，並檢查一些條件是否滿足，哪些條件會是什麼？ ->->-> ` - module map的對應模組紀錄是unlinked?`
<!--SR:!2023-10-06,8,250-->


#🧠 ES Module：如何避免N個不同模組會替相同模組做N個重複性實例化？假設使用module map＋上鎖/解鎖的機制，每一個首次要求做對應模組實例的任務會先對module map對應模組紀錄進行上鎖，並檢查一些條件是否滿足，若滿足的話，會做什麼 ->->-> `- 將module map的對應模組紀錄狀態更改：unlinked -> linking - 對module map的對應紀錄上解鎖 - 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；替輸出var變數宣告分配一塊記憶體，初始值為undefined - 替對應模組建立environment record -  藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record** - 替當前的模組處理 export 和 import：將export的識別字和import的識別字分別指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊 - 將module map的對應模組紀錄狀態更改：linking -> linked`
<!--SR:!2024-02-17,340,250-->


#🧠 ES Module：假如有N個模組，做完一個模組的實例化，會直接做它的evaluation嗎？ ->->-> `並不會，做完實例化並不會直接做evaluation，會等全部模組的instantiation 的做完才會做evaluation`
<!--SR:!2024-01-05,319,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
[[es-modules-a-cartoon-deep-dive(3) - Parsing 筆記]]
[[es-modules-a-cartoon-deep-dive(5) - Evaluation 筆記]]
References:
[[@linclarkESModulesCartoon]]
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]