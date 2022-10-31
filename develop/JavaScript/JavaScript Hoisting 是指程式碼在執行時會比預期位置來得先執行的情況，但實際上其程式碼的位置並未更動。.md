## 描述
[[@mdnTiShengHoistingShuYuBiao]] 所描述的：
> JavaScript **Hoisting** refers to the process whereby the interpreter appears to move the _declaration_of functions, variables or classes to the top of their scope, prior to execution of the code.

> Hoisting allows functions to be safely used in code before they are declared.

> Variable and class _declarations_ are also hoisted, so they too can be referenced before they are declared. Note that doing so can lead to unexpected errors, and is not generally recommended.

> 提升（Hoisting）是在 ECMAScript® 2015 Language Specification 裡面找不到的專有名詞。它是一種釐清 JaveScript 在執行階段內文如何運行的思路（尤其是在創建和執行階段）。然而，提升一詞可能會引起誤解：例如，提升看起來是單純地將變數和函式宣告，移動到程式的區塊頂端，然而並非如此。變數和函數的宣告會在編譯階段就被放入記憶體，但實際位置和程式碼中完全一樣。

重點：
- hoisting 並非實際上的技術用語，而是幫助人理解用的用語
- hoisting 起源於：
	- 人們會將JS程式碼的執行視為邊解析邊執行，不會想到JS的執行前會先經過編譯以及同時間分配記憶體，這就造成在執行時就已經呈現出 **部分程式碼是已經先比預期位置來得先執行的情況** ，比如說
		- var變數，在以下例子中的箭頭代表目前執行的行數，但執行到console時，理論上，印出的變數要等到執行下一行執行完畢，才會有記憶體空間，所以console的結果會報錯，但實際上結果會是看起來下一行的部分指令**先放在預期程式碼之前就被執行**，也就是記憶體分配的var test，等到真正執行下一行，只是看起來是在分配記憶體的情況下存放123
	```
	// expected case
	// some codes
	-> console.log(test) // print undefined
	var test = 123

	// actual case
	var test
	// some codes
	-> console.log(test)
	test = 123
	```
	- hoisting：程式碼在執行時是會先比預期位置來得先執行的情況，就叫做hoisting，被系統提前執行，但實際上並沒有在程式碼上調整位置
- 發生hoisting 的情況：var變數宣告、函式宣告
- 實際情況為：在編譯期間，會對var變數宣告、函式宣告做以下事情，在執行時就已經獲取對應的記憶體空間和初始值
	- 分配記憶體並放置初始值至對應記憶體，var拿到的初始值為undefined，函式拿到的初始值為存放函式內容的記憶體空間
- 優點：
	- 在正式使用特定程式碼下的識別字之前，就分配記憶體和指定初始值，最後讓識別字去對應記憶體區塊，以試著增加執行時的效能
- 缺點：
	- 易讀性較差
### 範例

函式宣告：在編譯期間，會將所有函式宣告分配一塊記憶體，其記憶體內容會是catName的函式內容，最後讓catName這識別字去對應其記憶體區塊，最後catName的呼叫會直接對應函式內容
```

catName("Tigger");
/*
上面程式的結果是: "My cat's name is Tigger"
*/

function catName(name) {
  console.log("My cat's name is " + name);
}

```

var變數宣告：在編譯期間，會將var變數宣告分配一塊記憶體，其記憶體內容會是undefined，最後讓test這識別字去對應其記憶體區塊，最後console.log(test)印出的值會是undefined
```
// some codes
console.log(test)
var test = 123
```

## 複習

#🧠 hoisting 在JS是指什麼？程式碼位置？ ->->-> `程式碼在執行時是會先比預期位置來得先執行的情況，就叫做hoisting，被系統提前執行，但實際上並沒有在程式碼上調整位置`
<!--SR:!2022-12-11,81,230-->

#🧠 發生hoisting 的JS碼會在程式碼上調整位置嗎？ ->->-> `並不會`
<!--SR:!2023-02-20,128,250-->

#🧠 hoisting 在JS是真實存在的技術嗎？為什麼？->->-> `並不是，人們會將JS程式碼的執行視為邊解析邊執行，不會想到JS的執行前會先經過編譯以及同時間分配記憶體，這就造成在執行時就已經呈現出 **部分程式碼是已經先比預期位置來得先執行的情況** `
<!--SR:!2022-12-31,79,230-->

#🧠 發生hoisting的JS碼會是哪些程式碼？ ->->-> `函式宣告、var變數宣告`
<!--SR:!2022-11-07,67,250-->

#🧠 const/let 變數宣告、函式expression會發生 JS上的hoisting 嗎？ ->->-> `並不會`
<!--SR:!2022-11-14,73,250-->

#🧠 JS的hoisting背後潛藏的技術是什麼？不是指字面上的意思  ->->-> `在編譯期間，會對var變數宣告、函式宣告做以下事情，在執行時就已經獲取對應的記憶體空間和初始值 - 分配記憶體並放置初始值至對應記憶體，var拿到的初始值為undefined，函式拿到的初始值為存放函式內容的記憶體空間`
<!--SR:!2022-11-15,74,250-->

#🧠 JS的hoisting優點是什麼？(效能) ->->-> `在正式使用特定程式碼下的識別字之前，就分配記憶體和指定初始值，最後讓識別字去對應記憶體區塊，以試著增加執行時的效能`
<!--SR:!2022-11-02,65,250-->

#🧠 JS的hoisting缺點是什麼？ ->->-> `易讀性較差`
<!--SR:!2023-03-22,146,250-->

#🧠 請問會印出什麼東西？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658494293/blog/javascript/hoisting/var-hoisting-example_ikc1rt.png) ->->-> `會印出undefined，這是因為在編譯期間就已經替var變數宣告分配記憶體，接著在賦予undefined這初始值，所以在執行前，test就是undefined的內容，只是還沒執行到修改123就先印出，所以為undefined`
<!--SR:!2022-11-14,73,250-->

#🧠 請問會印出什麼東西？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658494293/blog/javascript/hoisting/function-hoisting-example_hfomaw.png) ->->-> `My cat's name is Tigger，這是因為在編譯期間就已經function宣告分配記憶體，接著在賦予一塊記憶體空間以及放置對應函式內容至其記憶體，接著再接catName這識別字對應這函式，所以在執行前就已經定義好了，只是現在拿現有的識別字對應內容來呼叫，也就是拿目前函式內容呼叫。`
<!--SR:!2023-04-09,160,250-->

---
Status:  #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[JavaScript - var 變數是出自於ES6之前的變數型別，會依據所處環境來變動自身的scope為global scope或者function scope]]
References:
[[@mdnTiShengHoistingShuYuBiao]]