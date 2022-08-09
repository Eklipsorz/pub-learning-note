## 描述
[[@mdnExportJavaScriptMDN]] 所描述：
> 有兩種使用 export 的方式，**named** 與 **default**。每個模組中可以有多個 named exports, 但只能有一個 default export。每種 export 都對應到一個先前說的語法。

> - Named exports:
```
// 前面已經宣告的函式可以這樣輸出
export { myFunction };

// 輸出常數
export const foo = Math.sqrt(2); 
```

> -  預設 export （一個 js 檔案只能有一個）:    
```
export default function() {}
// 或是 'export default class {}'
// 結尾不用分號
```

> Named exports 在輸出多個值的時候很有用，在 import 的時候, 會強制根據使用相同的物件名稱. 但如果是 default export 則可以用任意的名字輸出.


重點：
- ES module的exports有兩種方式：
	- named export：強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字
	- default export：
		- 則是不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字
		- 引用當初exporting module所輸出(export)出來的識別字則是按照預設的引用方式來獲取對應識別字所存下的內容



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
References:
[[@mdnExportJavaScriptMDN]]
