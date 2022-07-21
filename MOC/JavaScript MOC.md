## 背景

- JavaScript 出生背景
[[JavaScript 是出自於網景和微軟的瀏覽器大戰所衍生出來的產品，主張允許使用者能對網頁進行互動並獲得對應互動的效果]]

- JavaScript 是什麼？
[[JavaScript 本身是操作DOM節點的語言以及每個DOM節點的事件綁定來實現客戶端能與網頁互動，而為了確保DOM節點不受race condition影響而設計成允許一個主執行緒來負責執行]]
[[JavaScript之所以為直譯語言，是原本就為了盡可能讓開發者快速進行網頁上開發好拓展網景瀏覽器的市場，同時也盡可能減少編譯時所帶來的額外成本]]
[[JavaScript 因應HTML5所提出的Web Worker標準而開放額外的API來讓JavaScript去調用來減緩單執行緒所產生出來的blocking問題]]

## 背景技術

[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[JavaScript Parsing中所要做的事情就是將tokenizing得到字串陣列轉換成代表合法句子的樹狀結構以及賦予其樹狀結構一些語意上的性質]]
[[JavaScript 會在編譯時期分配記憶體給函式宣告、var宣告、定義各種scope的execution context]]


- Execution Context
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
[[Execution Context 中的outer reference 適用以實現scope chain]]
- Lexical Evironment
[[Scope 是指某識別字對應特定實體的合法使用範圍，具體實現Scope的方式有Lexical Scope 和Dynam Scope]]
[[switch 若沒給每個case一個Execution context的話，switch帶來的Execution context會將能夠存取到的識別字紀錄起來]]
[[Global Execution Context 在creation phase建立對應GEC所擁有的environment record、this、outer，而在execution phase 是更新GEC內容(environment record)]]
[[Function Execution Context 在creation phase建立對應FEC所擁有的environment record、this、outer，而在execution phase 是更新FEC內容(environment record)]]

- 函式
[[JavaScript：函式宣告本身就是識別字去對應一塊儲存函式內容的物件，所以在執行之前的掃描就可以以識別字去對應其函式，且初始值會是其函式內容]]

- var
[[JavaScript - var 變數是出自於ES6之前的變數型別，會依據所處環境來變動自身的scope為global scope或者function scope]]

- truthy vs. falsy
[[CS - truthy 是形容某內容能夠在布林表達式內表達成true，falsy 則是形容某內容能夠在布林表達式表達成false]]

## 技術用語
- polyfill
[[polyfill 是一個依據正式規範來實現瀏覽器未曾實現功能的程式代碼]]

- shim
[[shim 是向舊版環境提供新功能的程式代碼，但沒有依據正式公佈的規範來實現]]



## 數字
- isNaN
[[Javascript的isNaN會將空字串當作數字0，其解法為先轉換數字型態與自己轉換前的值比對]]


## 字串
- 欄位值是否為空
[[Belazy - 如何判斷是否欄位值為空]]
- 字串內容是否為數字或者字串是否為數字字串
[[驗證字串內容原本是否為數字字串的方法就是先將比對值以Number轉換，接著再以其結果轉換String比對原本轉換前的內容是否一致，一致則為Number String]]


## 日期
- Date.parse()
[[Javascript - Date.parse() 是將輸入參數轉換成從1970,01.01 至指定參數之間的經過秒數(毫秒)]]


## Promise

- forEach 的callback 放入promise?
[[原生forEach 的callback並不支援promise為主的callback]] 


## 排序

- 原生sort
[[JavaScript Array.sort 需要一個比較標準compare來排序輪流對陣列的每個元素，不會是單純只排序一輪，而是按照目前陣列是否滿足標準才決定下一次的排序]]

## 物件

- this
[[this、self、me等關鍵字在電腦語言中是指目前執行的代碼屬於哪一個實體物件]]

[[this 關鍵字的歷史是輸入物件的指定屬性至方法、輸入指定物件至方法、不需要載入指定物件至方法，而將其改造成是以指定物件呼叫的方法]]



## 函式
[[javascript - function 語法有分為function declaration 、function expression]]