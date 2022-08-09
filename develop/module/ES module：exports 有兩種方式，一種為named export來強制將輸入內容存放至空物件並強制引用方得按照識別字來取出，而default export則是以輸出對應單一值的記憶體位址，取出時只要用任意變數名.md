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

syntax：
```
export { name1, name2, …, nameN };
export { variable1 as name1, variable2 as name2, …, nameN };
// 用 var, const 也通
export let name1, name2, …, nameN;
export let name1 = …, name2 = …, …, nameN;

// 底下的 function 用 class, function* 也可以
export default _expression_;
export default function (…) { … }
export default function name1(…) { … }

export { name1 as default, … };
export * from …;
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
```


重點：
- ES module的exports有兩種方式：
	- named export：
		- 強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字
		- 使用方式主要為兩種，會統一放在物件並拿識別名來當物件屬性管理，引用named export會獲取物件，接著按照export的識別字來從物件出
		```
		// way 1
		// export let/var variable = value1		
		// output: (實際存放)
		{
			variable: value1
		}
		// how to import 
		import { variable } from 'xxx'
		
		// way 2
		// export { property1, property2,.... }
		// output: (實際存放)
		{
			property1: value1,
			property2: value2,
			.
			.
		}

		// how to import
		import { property1, property2, .... } from 'xxx'
		```
	- default export：
		- 則是不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字
		- 引用當初exporting module所輸出(export)出來的識別字則是可用任意變數名稱去接收，接著系統按照預設的引用方式來讓變數名稱對應識別字所存下的內容
		- 使用方式主要為一種，會直接輸出該存放單一值的記憶體位址來處理，而引用時可以不必按照識別字來取用，只需要拿
	```
	// way 1
	// export default expression
	// output:
	variable: value
	// how to import
	import variable from 'xxx'(variable可以是任意名稱，但都會指向存放value的記憶體區塊)

	// way 2
	// export default function (…) { … }
	// how to import
	import xxxxyyyy from 'xxxx' (xxxxyyyy 可以是任意名稱，但都會指向函式物件)
	```

### 總結：
1. ES module： named exports 是什麼？ ->->-> `強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字``

2. default exports 是什麼？ ->->->  `不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字，引用當初exporting module所輸出(export)出來的識別字則是可用任意變數名稱去接收，接著系統按照預設的引用方式來讓變數名稱對應識別字所存下的內容`


## 複習
#🧠 ES module：有哪兩種方式來輸出(export)模組內容？ ->->-> `named export 和 default export`

#🧠 ES module： named exports 是什麼？ ->->-> `強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字`

#🧠 ES module： named exports 是強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字，具體如何實現？ ->->->`強制輸出的內容放置空物件中來當屬性，其中屬性名稱會是輸出的識別字，屬性值是對應識別字的內容，取出的時候就用物件存取屬性方式來取`

#🧠 ES module： default exports 是什麼？ ->->-> `不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字，引用當初exporting module所輸出(export)出來的識別字則是可用任意變數名稱去接收，接著系統按照預設的引用方式來讓變數名稱對應識別字所存下的內容`

#🧠 ES module：default exports是不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字，那麼具體如何實現？ ->->-> ``不強制開發者引用(import)識別字必須是當初exporting module所輸出(export)出來的識別字，而是將輸出內容以存放單一值的記憶體區塊來輸出，引用時則是以任意變數名稱參照著存放該值的記憶體區塊`
`

#🧠 請試著寫出exporting module來以named exports輸出特定property1和property2，並以importing module來引用這些property1、property2->->-> `exporting module: export { property1, property2,.... }, importing module: import { property1, property2, .... } from 'xxx'`

#🧠 請試著寫出exporting module來以default exports輸出特定variable，並以importing module來引用這些variable ->->-> `exporting module: export default expression, importing module: import variable from 'xxx'`

#🧠 ES module：使用default exports來輸出識別字，引用時得按照輸出時的識別字來對應嗎 ->->-> `不一定一樣，可以不一樣`

#🧠 ES module：使用named exports來輸出識別字，引用時得按照輸出時的識別字來對應嗎 ->->-> `得必須一樣，因為得用物件來存取以識別字名稱製作的屬性`


---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
References:
[[@mdnExportJavaScriptMDN]]
