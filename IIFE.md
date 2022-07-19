

## 描述





[[@mdnIIFEMDNWeb]] 所描述的IIFE
> An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined


```
// function IIFE
(function () {
  /* … */
})();
```


```
//  Anonymous function IIFE
(function () {
  /* … */
})();
```

```
//  Arrow function IIFE
(() => {
  /* … */
})();
```

```
//  Async IIFE
(async () => {
  /* … */
})();
```


> It is a design pattern which is also known as a Self-Executing Anonymous Function and contains two major parts:

> The first is the anonymous function with lexical scope enclosed within the Grouping Operator (). This prevents accessing variables within the IIFE idiom as well as polluting the global scope.

> The second part creates the immediately invoked function expression () through which the JavaScript engine will directly interpret the function.

重點：
- IIFE 是為了解決 JavaScript 在 **同一份DOM Document載入多個JS檔案而產生出全域污染問題** 而提出的概念
- 具體依據概念為：
	- 藉由scope分開來解決：憑藉function 可以將scope分成global scope 和 function scope
	- 以function作為基礎於內部進行函式擴充以此實現模組scope和global scope：具體是以function closure來打造專屬於特定模組下所能擁有的函式、資料，拿以下作為例子，xxx為模組，而xxx1和xxx2則是模組能提供的功能區塊，而data則是專屬於xxx模組下的資料
	```
	function xxx() {
		const data = ....
		return {
			function xxx1() {
				// execute some code with data
			},
			function xxx2() {
				// execute some code with data
			},
			.
			.
			.
		}
	}
	```



### IIFE 起初的問題和解決構想

[[@howardAnswerAdvancedJavaScript2012]] 所描述：

```javascript
function foo() {
  // Some code
}
foo();
```

> But this requires giving a name to the function, which is not always necessary. Using a named function also means at some future point the function could be called again which might not be desirable. By using an anonymous function in this manner you ensure it's only executed once.

> This syntax is invalid:

```javascript
function() {
  // Some code
}();
```

> Because you have to wrap the function in parentheses in order to make it parse as an expression. More information is here:[http://benalman.com/news/2010/11/immediately-invoked-function-expression/](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)


- 以function和function 的closure為主的模組還存在一些問題：
	- 以模組來說，呼叫方式很累贅：
		- 模組的載入執行方式只需要一個指令就應該完成：實際上還得宣告和呼叫這兩個指令才能完成
		- 預期是只需要執行一次就能使用它所擁有的功能代碼：可以通過函式名稱來重複呼叫
	- 所以預期是如下：
		- 定義完即為呼叫：實現模組的載入執行方式只需要一個指令就應該完成
		- 函式名稱是匿名或者隱藏：實現預期是只需要執行一次就能使用它所擁有的功能代碼
	```
	function () {
		const data = ....
		return {
			function xxx1() {
				// execute some code with data
			},
			function xxx2() {
				// execute some code with data
			},
			.
			.
			.
		}
	}()
	```

### function 主要分有宣告式和表達式

[[javascript - function 語法有分為function declaration 、function expression]]


### Grouping operator


> [[@mdnGroupingOperatorJavaScript]]

> The grouping operator `( )` controls the precedence of evaluation in expressions.


> The grouping operator consists of a pair of parentheses around an expression or sub-expression to override the normal operator precedence so that operators with lower precedence can be evaluated before an operator with higher precedence. As it sounds, it groups what's inside of the parentheses. 



```
const a = 1;
const b = 2;
const c = 3;

// default precedence
a + b * c     // 7
// evaluated by default like this
a + (b * c)   // 7

// now overriding precedence
// addition before multiplication
(a + b) * c   // 9

// which is equivalent to
a * c + b * c // 9
```


## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-07-22,3,250-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[IIFE]]
Links:
[[javascript - function 語法有分為function declaration 、function expression]]
References:
[[@BenAlmanImmediatelyInvoked]]
[[@mdnIIFEMDNWeb]]
[[@mdnGroupingOperatorJavaScript]]
[[@howardAnswerAdvancedJavaScript2012]]
