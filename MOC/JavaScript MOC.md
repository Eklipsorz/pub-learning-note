
## 背景技術

- Lexical Evironment
[[Scope 是指某識別字對應特定實體的合法使用範圍，具體實現Scope的方式有Lexical Scope 和Dynam Scope]]
[[switch 若沒給每個case一個Execution context的話，switch帶來的Execution context會將能夠存取到的識別字紀錄起來]]

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