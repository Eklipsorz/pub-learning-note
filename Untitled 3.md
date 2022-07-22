## 描述

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
	- hoisting：程式碼是已經先比預期位置來得先執行的情況，就叫做hoisting，被系統提前執行。
- 發生hoisting 的情況：var變數宣告、函式宣告
- 實際情況為所有var變數宣告和所有函式宣告會因為編譯時期就分配記憶體以及初始值，得以建立對應識別字和識別字對應的記憶體空間情況下的EC，並於真正執行時，可以來依據EC來獲取對應的var變數和函式宣告，即使他們的宣告程式碼並不是在使用之前，也會在開發者的眼中看起來就是其程式碼被拉升至使用之前，也就是hoisiting，但實際上並沒有調整位置
- 優點：
	- 在正式使用特定程式碼下的識別字之前，就分配記憶體和指定初始值，最後讓識別字去對應記憶體區塊
- 缺點：
	- 易讀差、
### 範例

函式宣告：在編譯期間，會將所有函式宣告和var宣告分配記憶體空間
```
function catName(name) {
  console.log("My cat's name is " + name);
}

catName("Tigger");
/*
上面程式的結果是: "My cat's name is Tigger"
*/
```


```
// some codes
-> console.log(test)
var test = 123
```

## 複習


---
Status:  #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[JavaScript - var 變數是出自於ES6之前的變數型別，會依據所處環境來變動自身的scope為global scope或者function scope]]
References: