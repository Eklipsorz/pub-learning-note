
## 描述
### Execution context 命名緣由
Execution 是指程式執行時的背景、過程，而context是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物，兩者合併起來就是程式執行時所在的場景，而這個場景可以解釋程式執行，換言之，execution context就是定義依照什麼樣的情況/狀況來定義/解釋如何執行。


context：是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物
> **the situation within which something exists or happens, and that can help explain it**


### 在JS上的Execution context
1. 在JavaScript中，會是引擎執行JavaScript的執行環境，其環境會由輔助引擎執行程式碼的內容所構成
2. 在JavaScript中，JavaScript引擎會於編譯時期：
	- 產生對應的bytecode，bytecode 主要會：
		- 負責定義每個Scope下的Execution Context所需要建立的資料
		- 負責定義如何執行其他語法
3. 負責定義每個Scope下的Execution Context所需要建立的資料：
	- 每一個宣告的記憶體分配該如何進行：將記憶體分配至var變數宣告、函式宣告，其初始值分別為undefined、函式內容
	- thisbinding 所需要的資料
	- outer reference 所需要的資料
	- 定義每個識別字和實體物件間的關係
4. JavaScript引擎會於將要執行時做：
	- 拿建立EC所需的資料和對應ByteCode去建立EC
5. JavaScript引擎在執行時做：
	- 以目前EC來執行，並根據目前EC狀況來更新EC
6. 舉例：
	 - GEC：當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，直到開始執行前就先以GEC資料來建立，並直接拿目前GEC和Code來執行，根據執行過程來更新GEC的內容
	 - FEC：當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，當JS引擎進入到Function執行時，就先於執行之前建立FEC，接著以FEC內容來執行和根據執行過程來更新FEC
	 - BEC(Block Execution Context)：當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，當JS引擎進入到Block執行，就先於執行之前建立BEC，接著以BEC內容來執行和根據執行過程來更新BEC內容


### 編譯至執行的順序為

1. 編譯時期：編譯ByteCode + 順便定義每個scope的EC所需要的資料
2. 快要執行時期：以編譯時期所獲取到的資料和對應ByteCode來建立EC
3. 執行階段：以目前EC來執行程式碼，並根據結果來更新EC

### 每個Execution Context 所面臨的階段
> When the JavaScript engine executes the JavaScript code, it creates execution contexts. Each execution context has two phases: the creation phase and the execution phase.

每一個execution context都具有兩個階段：
- creation phase：execution context建立的階段，會拿編譯時期的資訊來建立EC所會有 identifier : instance、this、outer reference。
- execution phase：程式依據著初期設定的execution context執行的時候，在這時候會邊依據邊把需要更動的資訊紀錄至context

### Execution Context 種類
Execution Context主要共分為三種：當JS檔案進行編譯時，就會對各種scope建立對立的EC，分別為GEC和FEC

- Global Execution Context(GEC): 以程式碼全域所在的程式碼為主來構成，不包含function的內部執行、block的內部執行。

- Function Execution Context(FEC):  通常會是function關鍵字以及{}來構築

```
let a = 0

function test(num) {
	console.log(num)
}

test(a)
```

- Block Execution Context (BEC)：以{}所建立的Execution Context，沒function的前綴。

## 複習

#🧠 Execution context 命名緣由 是什麼？->->-> `Execution 是指程式執行時的背景、過程，而context是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物，兩者合併起來就是程式執行時所在的場景，而這個場景可以解釋程式執行，換言之，execution context就是定義依照什麼樣的情況/狀況來定義/解釋如何執行。`
<!--SR:!2024-09-17,498,250-->

#🧠 在JS上的Execution context 會是指什麼？ ->->-> `在JavaScript中，會是引擎執行JavaScript的執行環境，其環境會由輔助引擎執行程式碼的內容所構成`
<!--SR:!2024-12-23,516,230-->

#🧠 在JS引擎一執行檔案時，會做些什麼來執行？->->-> `1. 編譯時期：編譯ByteCode + 順便定義每個scope的EC所需要的資料2. 快要執行時期：以編譯時期所獲取到的資料和對應ByteCode來建立EC 3. 執行階段：以目前EC來執行程式碼，並根據結果來更新EC`
<!--SR:!2024-12-29,517,248-->

#🧠 JavaScript 會於編譯時期確定每個Scope和對應的EC嗎？具體如何確定 ->->-> `會，具體的話，會於編譯時期透過生成對應ByteCode來準備建立EC所需要的資料`
<!--SR:!2025-02-03,536,248-->

#🧠 JavaScript 會於編譯時期就建立EC嗎？為何？->->-> `不會，編譯時期只是生成建立EC的指令和所需的資料`
<!--SR:!2024-01-18,121,228-->

#🧠 JavaScript 會於何時建立EC ->->-> `編譯時期後，快要執行對應的Scope前就會建立並執行`
<!--SR:!2023-10-22,255,248-->

#🧠 JavaScript 引擎於完整的編譯時期和執行對應scope之前的時期會替EC做什麼？ ->->-> `1. 編譯時期：編譯ByteCode + 順便定義每個scope的EC所需要的資料 2. 快要執行時期：以編譯時期所獲取到的資料和對應ByteCode來建立EC`
<!--SR:!2023-11-08,100,228-->

#🧠 請完整說明負責定義每個Scope下的Execution Context所需要建立的資料之ByteCode是什麼？ 具體說明會建立哪些資料 ->->-> `		- 負責定義每個Scope下的Execution Context所需要建立的資料- 負責定義如何執行其他語法。其中定義EC所需要建立的資料有：	- 每一個宣告的記憶體分配該如何進行：將記憶體分配至var變數宣告、函式宣告，其初始值分別為undefined、函式內容 - thisbinding 所需要的資料 - outer reference 所需要的資料 - 如何定義每個識別字和實體物件間的關係`
<!--SR:!2023-10-16,247,247-->


#🧠 請完整說明JavaScript 引擎在編譯時期會建立所有Scope種類的EC嗎？具體說明？ ->->-> `並不會直接建立，會於編譯時期定義每個Scope種類所需要建立的資料和對應ByteCode。`
<!--SR:!2023-10-26,243,248-->


#🧠 請完整說明JavaScript 引擎在何時建立任意種類的EC (block EC、global EC、function EC)？ ->->-> `快要執行對應Scope的EC前`
<!--SR:!2024-12-24,517,248-->

#🧠 請完整說明JavaScript 引擎在編譯時期、快要執行時期、執行時期替EC做了什麼？ ->->-> `在JavaScript中，JavaScript引擎會於編譯時期： 產生對應的bytecode，bytecode 主要會： - 負責定義每個Scope下的Execution Context所需要建立的資料 - 負責定義如何執行其他語法。接著將要執行時，拿建立EC所需的資料和對應ByteCode去建立EC、以目前EC來執行，並根據目前EC狀況來更新EC`
<!--SR:!2024-12-14,508,248-->


#🧠 JavaScript 引擎於執行時期會替EC 做什麼？->->-> ` 以目前EC來執行，並根據目前EC狀況來更新EC`
<!--SR:!2023-10-14,266,246-->

#🧠 請完整說明JavaScript 引擎在編譯時期、快要執行時期、執行時期替Global Scope的程式碼做了什麼樣的EC？ ->->-> `當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，直到開始執行前就先以GEC資料來建立，並直接拿目前GEC和Code來執行，根據執行過程來更新GEC的內容`
<!--SR:!2025-03-03,564,248-->


#🧠 請完整說明JavaScript 引擎在編譯時期、快要執行時期、執行時期替Function Scope的程式碼做了什麼樣的EC？ ->->-> `當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，當JS引擎進入到Function執行時，就先於執行之前建立FEC，接著以FEC內容來執行和根據執行過程來更新FEC`
<!--SR:!2023-10-24,257,248-->


#🧠 請完整說明JavaScript 引擎在編譯時期、快要執行時期、執行時期替Block Scope的程式碼做了什麼樣的EC？ ->->-> `BEC(Block Execution Context)：當JS引擎進入到檔案執行時，就先進入編譯時期並準備各種資料和對應ByteCode來方便未來建立各種EC，當JS引擎進入到Block執行，就先於執行之前建立BEC，接著以BEC內容來執行和根據執行過程來更新BEC內容`
<!--SR:!2024-12-30,518,248-->



#🧠 JS：每個Execution Context 所面臨的階段是什麼？ ->->-> `- creation phase：execution context建立的階段，會拿編譯時期的資訊來建立EC所會有 identifier : instance、this、outer reference。 - exection phase：程式依據著初期設定的execution context執行的時候，在這時候會邊依據邊把需要更動的資訊紀錄至context`
<!--SR:!2025-03-08,536,248-->


#🧠 JS：Execution Context 種類 (共三種：Block、Global、Function) ->->-> `Global Execution Context(GEC): 以程式碼全域所在的程式碼為主來構成，不包含function的內部執行、block的內部執行。 - Function Execution Context(FEC):  通常會是function關鍵字以及{}來構築，在這裡當GEC呼叫function並執行function時或者執行對應block的內部執行時就會以當時所要執行的內部程式碼為範疇來建構，比如説：當GEC呼叫了test(a)時，系統就便會執行test內部的第一行，此時就會進入該函式的FEC並開始進入creation phase和execution phase - 以{}所建立的Execution Context：通常會是由一對{}所建立，如同function execution context，只要一進入就會進入該context的creation  phase，然後建立完之後就進入execution phase`
<!--SR:!2023-11-24,318,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[Execution Context 中的outer reference 適用以實現scope chain]]
References: