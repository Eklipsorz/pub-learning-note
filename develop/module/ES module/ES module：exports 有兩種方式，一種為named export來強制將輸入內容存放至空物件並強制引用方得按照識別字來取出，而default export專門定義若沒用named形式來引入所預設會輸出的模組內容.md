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
		- 以物件形式來輸出模組內容，其屬性為主要內容，這使得每個主要內容都會被特定屬性名稱給綁定或者替該內容命名為該屬性名稱，而命名為named import
		- 引入方必須以物件形式的特定屬性名稱才能取得內容
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
		- 專門定義若沒用named形式來引入所預設會輸出的模組內容，即不以物件形式來引入其模組，而是改以單一值來引入。
		- 形式上不會以物件來輸出，而是輸出會以單一值來輸出
		- exporting module所輸出的內容是(識別字所對應的)單一值，importing module則是可用任意變數來分配空間來引用輸出的單一值
		- 使用方式主要為一種，會直接輸出該存放單一值，而引用時可以不必按照識別字來取用，只需要拿
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
1. ES module： named exports 是什麼？  `	- 以物件形式來輸出模組內容，其屬性為主要內容，這使得每個主要內容都會被特定屬性名稱給綁定或者替該內容命名為該屬性名稱，而命名為named import - 引入方必須以物件形式的特定屬性名稱才能取得內容`


2. default exports 是什麼？  `- 專門定義若沒用named形式來引入所預設會輸出的模組內容，即不以物件形式來引入其模組，而是改以單一值來引入。 - 形式上不會以物件來輸出，而是輸出會以單一值來輸出`



3. ES module：default exports 和 named exports  若擺放在同一個模組檔案，引入方兩邊都能引入，那麼如何引入？？ `若要引入named exports，就以物件的解構來引入，若要引入default exports，就以單一值的形式來存放，如同變數儲存特定內容`



## 複習
#🧠 ES module：有哪兩種方式來輸出(export)模組內容？ ->->-> `named export 和 default export`
<!--SR:!2024-01-23,123,230-->

#🧠 ES module：相對於default export，named export會輸出和引入會是？ ->->-> `	- 以物件形式來輸出模組內容，其屬性為主要內容，這使得每個主要內容都會被特定屬性名稱給綁定或者替該內容命名為該屬性名稱，而命名為named import - 引入方必須以物件形式的特定屬性名稱才能取得內容`
<!--SR:!2023-12-06,93,230-->

#🧠 ES module： named exports 是強制開發者要引用(import)的識別字必須是當初exporting module所輸出(export)出來的識別字，具體如何實現？ ->->->`強制輸出的內容放置空物件中來當屬性，其中屬性名稱會是輸出的識別字，屬性值是對應識別字的內容，取出的時候就用物件存取屬性方式來取`
<!--SR:!2024-07-08,420,250-->

#🧠 ES module：相對於named export，default exports會輸出和引入會是？ ->->-> `- 專門定義若沒用named形式來引入所預設會輸出的模組內容，即不以物件形式來引入其模組，而是改以單一值來引入。 - 形式上不會以物件來輸出，而是輸出會以單一值來輸出`
<!--SR:!2024-08-21,394,230-->

#🧠 ES module：default exports 和 named exports  若擺放在同一個模組檔案，請問引入方還能正常引入嗎？ 那麼具體可引入哪種？->->-> `可以，兩邊都可以`
<!--SR:!2023-10-28,96,230-->

#🧠 ES module：default exports 和 named exports  若擺放在同一個模組檔案，引入方兩邊都能引入，那麼如何引入？？->->-> `若要引入named exports，就以物件的解構來引入，若要引入default exports，就以單一值的形式來存放，如同變數儲存特定內容`
<!--SR:!2024-11-26,491,250-->

#🧠 請試著寫出exporting module來以named exports輸出特定property1和property2，並以importing module來引用這些property1、property2->->-> `exporting module: export { property1, property2,.... }, importing module: import { property1, property2, .... } from 'xxx'`
<!--SR:!2024-02-22,338,250-->

#🧠 請試著寫出exporting module來以default exports輸出特定variable，並以importing module來引用這些variable ->->-> `exporting module: export default expression, importing module: import variable from 'xxx'`
<!--SR:!2023-12-20,300,250-->

#🧠 ES module：使用default exports來輸出識別字，引用時得按照輸出時的識別字來對應嗎 ->->-> `不一定一樣，可以不一樣`
<!--SR:!2025-06-14,625,250-->

#🧠 ES module：使用named exports來輸出識別字，引用時得按照輸出時的識別字來對應嗎 ->->-> `得必須一樣，因為得用物件來存取以識別字名稱製作的屬性`
<!--SR:!2024-04-27,378,250-->

#🧠 ES module：同一個模組的export來說，named export形式可以輸出幾個？default export形式可以輸出幾個 ->->-> `named 可以輸出多個named形式，default形式只能允許一個`
<!--SR:!2023-12-16,103,230-->

#🧠 ES module：同一個模組的export來說 ，named export形式可以輸出多個嗎？->->-> `可以`
<!--SR:!2024-11-27,492,250-->

#🧠 ES module：同一個模組的export來說 ，default export形式可以輸出多個嗎？為什麼？->->-> `不可以，default本就只是預設的輸出方式，本身並不會輸出多個default export的必要`
<!--SR:!2023-10-13,81,210-->

---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
[[ES module：在named export中可允許匯出的形式分別有單一宣告語句來匯出和以物件形式來匯出，兩者皆會試著將多個export的內容合併成一個結果物件來匯出]]
References:
[[@mdnExportJavaScriptMDN]]
