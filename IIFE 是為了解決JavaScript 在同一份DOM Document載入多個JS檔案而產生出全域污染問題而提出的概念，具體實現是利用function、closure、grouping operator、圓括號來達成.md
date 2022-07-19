

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
- IIFE (Immediately Invoked Function Expression) 是為了解決 JavaScript 在 **同一份DOM Document載入多個JS檔案而產生出全域污染問題** 而提出的概念
- IIFE實際上是一個function一被定義/宣告就直接執行
- 設計構想為：Ben Alman，並非標準下所提供的語法
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
	- grouping operator 強制將function 轉換成 function expression 來看待
	- () 將轉換後的function expression以function來呼叫


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


模組化設定的目標：
1. 只需要載入/執行一次，就能用對應功能 
2. 載入動作只需要一個指令就能完成

然而實際上：
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


#### 面臨的問題

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

解析器會因為一開始沒在function 之前遇到可將function 視為 function expression 的話，解析器會直接把function declaration來解析function，而它沒有函式名稱而報錯

為了強制將可以被當作expression而被誤會成declaration的function轉成function expression，會使用()這個grouping expression來強制系統先以expression 來看待function，也就是如同下面的形式：當解析器讀到括號時，會先以expression的形式來執行其包含內容，此時內容是function(){}，那麼就會使該function轉換成function expressio

```
(function (){
	// some code
})
// grouping operator result
function () {

}
```

接著再透過expression之後放置圓括號的特性就能讓轉換成function expression的function以被呼叫的函式來執行，並將圓括號內的參數視為函式要用的參數來使用
```
(function () {
....
})()
```

### function 主要分有宣告式和表達式

[[javascript - function 語法有分為function declaration 、function expression]]

### expression 之後放置括號的作用
```
 function(){ /* code */ }(); // SyntaxError: Unexpected token (
```


> Interestingly enough, if you were to specify a name for that function and put parens immediately after it, the parser would also throw a SyntaxError, but for a different reason. 


重點：
- 若將圓括號()放置在expression之後，就會告知解析器expression是一個被呼叫的function，而括號()裡頭的參數將會是該function會使用到的參數



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


重點：
- grouping operator 是一種運算子，主要參數為一個expression，形式會是如下，最後回傳的值會是expression
```
(expression)
```
- 用途為：
	- 強制使語法轉換成expression 形式
	- 在混雜其他expression中，會將指定的expression的執行權提高至最高，換言之，優先被解析器邊解析邊執行，案例如下：在這裡 是由1、2、3皆為expression，而+、＊則是搭配著兩個參數來構成expression，可以透過()告知系統先執行哪個expression，比如(1+2)、或者是(2\*3)
	```
	console.log(1 + 2 * 3); // 1 + 6
	// expected output: 7
	
	console.log(1 + (2 * 3)); // 1 + 6
	// expected output: 7

	console.log((1 + 2) * 3); // 3 * 3
	// expected output: 9

	console.log(1 * 3 + 2 * 3); // 3 + 6
	// expected output: 9
	```
## 複習
#🧠 IIFE (Immediately Invoked Function Expression) 為了解決什麼樣的問題而被提出的？ ->->-> `JavaScript 在 **同一份DOM Document載入多個JS檔案而產生出全域污染問題** 而提出的概念`

#🧠  IIFE (Immediately Invoked Function Expression) 具體是什麼？ ->->-> `IIFE實際上是一個function一被定義/宣告就直接執行`


#🧠 IIFE (Immediately Invoked Function Expression)是官方標準所提出的？ ->->-> `Ben Alman，並非標準下所提供的語法`


#🧠  IIFE (Immediately Invoked Function Expression) 大致上使用了哪些技術->->-> `藉由scope分開來解決：憑藉function 可以將scope分成global scope 和 function scope、以function作為基礎於內部進行函式擴充以此實現模組scope和global scope：具體是以function closure來打造專屬於特定模組下所能擁有的函式、資料，拿以下作為例子，xxx為模組，而xxx1和xxx2則是模組能提供的功能區塊，而data則是專屬於xxx模組下的資料、grouping operator 強制將function 轉換成 function expression 來看待、() 將轉換後的function expression以function來呼叫`

#🧠 IIFE (Immediately Invoked Function Expression) 為何採用function ->->-> `藉由scope分開來解決：憑藉function 可以將scope分成global scope 和 function scope`

#🧠 IIFE (Immediately Invoked Function Expression)  為何使用closure ? 可以的話，舉一個例子來表示 ->->-> `具體是以function closure來打造專屬於特定模組下所能擁有的函式、資料，拿以下作為例子，xxx為模組，而xxx1和xxx2則是模組能提供的功能區塊，而data則是專屬於xxx模組下的資料 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658247098/blog/javascript/lexical%20scope/closure-result_xtdlgu.png)`


#🧠 IIFE (Immediately Invoked Function Expression) 大致上若只使用到藉由scope分開來解決和closure的話，還會遇到什麼樣的問題 ->->-> `主要會`



#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``



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
