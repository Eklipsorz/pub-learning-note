
## 描述
### Execution context 命名緣由
Execution 是指程式執行時的背景、過程，而context是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物，兩者合併起來就是程式執行時所在的場景，而這個場景可以解釋程式執行，換言之，execution context就是定義依照什麼樣的情況/狀況來定義/解釋如何執行。


context：是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物
> **the situation within which something exists or happens, and that can help explain it**


### 在JS上的Execution context
1. 在JavaScript中，會是引擎執行JavaScript的執行環境，其環境會由輔助引擎執行程式碼的內容所構成
2. 在JavaScript中，當JavaScript引擎開始解析執行某個檔案上的JS程式碼時，：
	 - 先替該檔案建立Global Execution Context(GEC)來設定執行會需要的環境變數以及儲存過程，當建立完之後，引擎就隨後執行JS程式碼，便以該context為基礎來執行以及更新context所需的資訊至context


### 每個Execution Context 所面臨的階段
> When the JavaScript engine executes the JavaScript code, it creates execution contexts. Each execution context has two phases: the creation phase and the execution phase.

每一個execution context都具有兩個階段：
- creation phase：execution context建立的階段或者程式剛開始被執行的階段，此階段會掃描該context的程式碼並解析其識別字，並於context紀錄其結果
- exection phase：程式依據著初期設定的execution context執行的時候，在這時候會邊依據邊把需要更動的資訊紀錄至context

### Execution Context 種類
Execution Context主要共分為兩種：

- Global Execution Context(GEC): 以程式碼全域所在的程式碼為主來構成，不包含function的內部執行、block的內部執行。

- Function Execution Context(FEC):  通常會是function關鍵字以及{}來構築，在這裡當GEC呼叫function並執行function時或者執行對應block的內部執行時就會以當時所要執行的內部程式碼為範疇來建構，比如説：當GEC呼叫了test(a)時，系統就便會執行test內部的第一行，此時就會進入該函式的FEC並開始進入creation phase和execution phase

```
let a = 0

function test(num) {
	console.log(num)
}

test(a)
```

- 以{}所建立的Execution Context：通常會是由一對{}所建立，如同function execution context，只要一進入就會進入該context的creation  phase，然後建立完之後就進入execution phase

## 複習

#🧠 Execution context 命名緣由 是什麼？->->-> `Execution 是指程式執行時的背景、過程，而context是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物，兩者合併起來就是程式執行時所在的場景，而這個場景可以解釋程式執行，換言之，execution context就是定義依照什麼樣的情況/狀況來定義/解釋如何執行。`
<!--SR:!2022-08-02,28,250-->

#🧠 在JS上的Execution context 會是指什麼？ ->->-> `在JavaScript中，會是引擎執行JavaScript的執行環境，其環境會由輔助引擎執行程式碼的內容所構成`
<!--SR:!2022-08-05,13,230-->

#🧠 在JS引擎一執行檔案時，會先建立什麼樣的Context ? 又是如何做啥（建立和更新)->->-> `先替該檔案建立Global Execution Context(GEC)來設定執行會需要的環境變數以及儲存過程，當建立完之後，引擎就隨後執行JS程式碼，便以該context為基礎來執行以及更新context所需的資訊至context`
<!--SR:!2022-08-04,11,230-->

#🧠 JS：每個Execution Context 所面臨的階段是什麼？ ->->-> `- creation phase：execution context建立的階段或者程式剛開始被執行的階段，此階段會掃描該context的程式碼並解析其識別字，並於context紀錄其結果 - exection phase：程式依據著初期設定的execution context執行的時候，在這時候會邊依據邊把需要更動的資訊紀錄至context`
<!--SR:!2022-07-27,28,250-->

#🧠 JS：Execution Context 種類 (共三種：Block、Global、Function) ->->-> `Global Execution Context(GEC): 以程式碼全域所在的程式碼為主來構成，不包含function的內部執行、block的內部執行。 - Function Execution Context(FEC):  通常會是function關鍵字以及{}來構築，在這裡當GEC呼叫function並執行function時或者執行對應block的內部執行時就會以當時所要執行的內部程式碼為範疇來建構，比如説：當GEC呼叫了test(a)時，系統就便會執行test內部的第一行，此時就會進入該函式的FEC並開始進入creation phase和execution phase - 以{}所建立的Execution Context：通常會是由一對{}所建立，如同function execution context，只要一進入就會進入該context的creation  phase，然後建立完之後就進入execution phase`
<!--SR:!2022-09-05,51,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: