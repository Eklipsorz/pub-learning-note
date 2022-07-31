## 描述

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
	- 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體；
	- 設定export 和 import 指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊，這技術稱之為live bindings
	- 建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件
	- 藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record**

3. 限制：相對來說，ES 模組會使用live bindings技術來讓模組間的export和import所指的識別字都指向同個記憶體區塊，這表示只要在模組上更改值，就會使用import的那一方拿到變更後的值，但只有exporting module那一方才能更改對應的值，importing module不能夠更改import識別字上的對應實體物件(記憶體內容)，最多只能增加屬性至物件上。

![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_04-768x316.png)

> The reason to have live bindings like this is then you can wire up all of the modules without running any code. This helps with evaluation when you have cyclic dependencies, as I’ll explain below.

### 為何避免多個不同模組會替相同模組而做的重複性實例化
N個模組索要模組做實例化代表有N個任務會同時索要模組做實例化，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時要求模組實例化，但若模組是相同的話，將會有N個相同模組下的實例，然而，實際上也只需要一個實例，所以這對於瀏覽器來說，由於多做實例而使效能衰減

#### 如何避免多個不同模組會替相同模組而做的重複性實例化？
使用module map＋鎖的機制，只有一個任務能夠負責特定模組檔案的實例，建立完實例就在module map以模組所在的URL作為索引來標記 **對應record上的environment屬性對應著模組的environment record**，接著執行evaluation，執行完之後就便允許其他任務能夠從module map存取對應模組狀態來要不要做實例化：
	- 若對應模組狀態顯示**對應record上的environment屬性對應著模組的environment record**，那麼任務當下就從record取出該模組下所對應的記憶體位置作為引入。
	- 若找不到，任務就當那個第一個實例特定模組的任務，剩下要做同樣事情的任務就停留在正要讀取record的時候，由第一個任務來完成實例、標記 **對應record上的environment屬性對應著模組的environment record**，接著執行evaluation，最後解鎖讓其他任務去檢查


## 複習
#🧠 ES Module： 每一個模組的實例會如何做？(提示：有四個步驟)->->-> `1. 會分配記憶體來提供每一個實例所要輸出的內容，並分配初始值：輸出函式就分配存放函式內容的記憶體 2. 設定export 和 import 指向於模組A所要輸出的內容以及其他模組依賴於模組A的輸出內容，兩者都會指向存放目前模組A的輸出內容之記憶體區塊，這技術稱之為live bindings、建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件、3. 建立module environment record來紀錄每個模組下的每個識別字以及對應識別字的實體物件 4. 藉由模組所在的位置來從module map上找到對應模組的紀錄，並將**module record 的屬性environment去指向module environment record**`




#🧠 ES Module：如何利用模組依賴關係圖來挑選哪個模組進行實例化？ ->->-> `具體而言，會先挑沒使用任何依賴或者使用著已經完成實例化模組的模組來進行實例化，而模組依賴關係圖底部或者越往底部正是那些，所以會使用Depth First Post-Order Travesal來從模組依賴關係圖的起始點轉移至圖的底部，試圖先實例化沒有任何依賴的模組群組A，接著實例化依賴著模組群組A的模組群組B，然後一直往上實例，直到遍歷完所有模組並做完所有模組的實例`


#🧠 用這兩張圖來說明ES module 的實例化，其中右邊是main.js，左邊由先至後是counter.js和render.js，主要main.js會依賴這兩個模組![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_01-768x316.png) ![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_02-768x316.png)->->-> ``

#🧠 ES module的live bindings是什麼？ ->->-> `概念上會是exporting module輸出的識別字和importing module引用的識別字都各自指向相同的記憶體區塊，當exporting module改變識別字對應的記憶體區塊內容，importing module就會馬上看到其識別字對應的(記憶體區塊)內容`
`

#🧠 ES module：一旦建立live bindings，會有哪些限制 ->->-> `相對來說，ES 模組會使用live bindings技術來讓模組間的export和import所指的識別字都指向同個記憶體區塊，這表示只要在模組上更改值，就會使用import的那一方拿到變更後的值，但只有exporting module那一方才能更改對應的值，importing module不能夠更改import識別字上的對應實體物件(記憶體內容)，最多只能增加屬性至物件上。`


#🧠 ES Module： 為何避免多個不同模組會替相同模組而做的重複性實例化 ->->-> `N個模組索要模組做實例化代表有N個任務會同時索要模組做實例化，若執行緒數量和實際核心數夠讓每個任務執行的話，每個任務將會以執行緒同時要求模組實例化，但若模組是相同的話，將會有N個相同模組下的實例，然而，實際上也只需要一個實例，所以這對於瀏覽器來說，由於多做實例而使效能衰減`


#🧠 ES Module： 如何避免多個不同模組會替相同模組而做的重複性實例化？ ->->-> `使用module map＋鎖的機制，只有一個任務能夠負責特定模組檔案的實例，建立完實例就在module map以模組所在的URL作為索引來標記 **對應record上的environment屬性對應著模組的environment record**，接著執行evaluation，執行完之後就便允許其他任務能夠從module map存取對應模組狀態來要不要做實例化：- 若對應模組狀態顯示**對應record上的environment屬性對應著模組的environment record**，那麼任務當下就從record取出該模組下所對應的記憶體位置作為引入。 - 若找不到，任務就當那個第一個實例特定模組的任務，剩下要做同樣事情的任務就停留在正要讀取record的時候，由第一個任務來完成實例、標記 **對應record上的environment屬性對應著模組的environment record**，接著執行evaluation，最後解鎖讓其他任務去檢查`



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
References:
[[@linclarkESModulesCartoon]]