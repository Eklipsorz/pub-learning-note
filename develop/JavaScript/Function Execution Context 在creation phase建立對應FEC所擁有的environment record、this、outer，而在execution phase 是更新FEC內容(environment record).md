## 描述

這裡的概念以ECMA2015-ECMA2019為主，Function Execution Context 簡稱為FEC。
### FEC - creation phase
1. 發生時間點：在編譯時期先對所有EC準備建立EC所需的資料和對應的ByteCode後，並於執行之前先執行ByteCode來建立FEC
2. FEC範圍：以區塊內或者函式內的所有區域變數、函式為主、不包含額外用區塊和函式包住的程式碼
3. 製作流程：
- 建立this物件並決定this參照於誰：
	- 在這裡建立完會依據哪個物件呼叫該函式，而決定FEC的this為那個物件。
	- 若沒有物件呼叫就依照**outer reference**所指向的EC所擁有的this來決定this為誰
	```
	this = otherEC.this
	```
- 建立Arguments物件來儲存賦予對應函數的參數：主要會包含參數、參數長度，以下面函式呼叫為例，當呼叫並執行test函式的第一段前會先建立對應的FEC，其中會先建立Arguments物件儲存1、3、4以及參數長度，其中0-2為代表著test呼叫中的argument1至argument3，而length則是代表著參數長度(如result那樣呈現)，而Arguments所儲存的變數皆為let類型的變數宣告，所以會將Arguments放在FEC中的LexicalEnvironment區塊。

```
function test(a, b, c) {
	....
}

test(1, 3, 4)

// result
Arguments: {0: 1, 1: 3, 2: 4,length: 3},
```

- 建立屬於FEC的Lexical Environment：主要分為LexicalEnvironment、VariablEenvironment，如同GEC那樣，唯二不同的事情就是：第一、outer會是指向呼叫該EC的EC，也就是代表從全域呼叫的GlobalExectionContext或者代表從其他函式呼叫的EC，第二、ThisBinding會是依據著是否為箭頭函式，而採用語彙綁定或者依據傳統的explicit binding、new binding、default binding、implicit binding

```

FunctionExectionContext = {
	LexicalEnvironment: {
		EnvironmentRecord: {
			type: "Declarative",
			// Identifier bindings go here
		}
		outer: <null>,
		ThisBinding: <Global Object>
	},

	VariableEnvironment: {
		EnvironmentRecord: {
			// Identifier bindings go here
		}
		outer: <null>,
		ThisBinding: <Global Object>
	}
}
```

- LexicalEnvironment 從FEC收集函式宣告、let/const形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中，

```
identifier: <function>
identifier: <const variable>
identifier: <let variable>
```

剩餘就如同GEC中的LexicalEnvironment那樣

```
FunctionExectionContext = {

	LexicalEnvironment: {

		EnvironmentRecord: {
			Type: "Object",
			// Identifier bindings go here
			identifier1: <uninitialized>,
			identifier2: <uninitialized>,
			identifier3: <func>
		}

		outer: <null>,
		ThisBinding: <Global Object>
	}
}
```

- VariablEenvironment：從GEC收集var形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中，

```
identifier: <var variable>
```

剩餘就如同GEC中的VariablEenvironment那樣

```
FunctionExectionContext = {
	VariableEnvironment: {

		EnvironmentRecord: {
			Type: "Object",
			// Identifier bindings go here
			identifier1: undefined
		}

		outer: <null>,
		ThisBinding: <Global Object>
	}
}
```


### FEC - execution phase
1. 建立完FEC後，JavaScript 引擎隨後就會在FEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context

> JavaScript Engine executes the code line by line

2. 在這裏主要會做：
	- 更新Lexical Environment的對應值

#### argument object in FEC vs global object in GEC

[[@JavaScriptDeZhiXingJieDuanExecutionContext]]
> 和 Global Execution Context 的區別，引用文獻解釋的比較清楚 :

> The Function Execution Context is similar to the Global Execution Context, but instead of creating the `global` object, _**it creates the `arguments` object that contains a reference to all the parameters passed into the function.**_  
> (引用自 JavaScript Execution Context )

> 簡而言之，Execution Context在 creation phase 創造的不是`window`，而是**欲傳進函式的參數`arguments`物件。**

> 於是我們在 Function Execution Context 在 _creation phase_ 會變成下列的狀態:
```
global object ：arguments
this：window
```


重點：
- 在Global Execution Context中，會建立一個global object來標記該執行環境是隸屬於誰並以其資訊來決定環境、如何執行內容：
	- 瀏覽器：window物件來設定，其代表對應畫面的呈現元件
	- Node.js：global 物件來設定，其代表執行環境本身
- 在Function Execution Context中，會建立一個argument object來標記該執行環境是隸屬於誰並以其資訊來決定環境、如何執行內容：
	- argument object 本身會是想傳進函式的參數，並在執行階段時使用和存取
	- argument object 本身是參數，但不會在FEC建立階段替函式內存放參數的識別字分配值，而是看是否為var形式還是let，來決定識別字和記憶體區塊的對應關係
	- 舉例：
```
function test(a, b, c) {
	....
}

test(1, 3, 4)

// result
Arguments: {0: 1, 1: 3, 2: 4,length: 3},
```

## 複習

#🧠 在Global Execution Context 中的global object是什麼？ ->->-> `標記該執行環境是隸屬於誰並以其資訊來決定環境、如何執行內容的物件`

#🧠 在Function Execution Context 中的argument object是什麼以及其用途為何？ ->->-> `標記該執行環境是隸屬於誰並以其資訊來決定環境、如何執行內容的物件`

#🧠 在Function Execution Context 中的argument object 會是什麼樣子，以test(1, 3, 4)為例 ->->-> `Arguments: {0: 1, 1: 3, 2: 4,length: 3},`

#🧠 function test(a, b, c) {}; test(1, 3, 4); 請問a、b、c在FEC建立的狀況為何->->-> `a: undefined、b：undefined、c：undefined`

#🧠 在Function Execution Context中，argument object 本身會是想傳進函式的參數，並在執行階段時使用和存取，請問在FEC建立階段會是如何決定存取參數的識別字和其記憶體之間對應關係->->-> `不會在FEC建立階段替函式內存放參數的識別字分配值，而是看是否為var形式還是let，來決定識別字和記憶體區塊的對應關係`


#🧠 在Function Execution Context中， argument object在FEC建立時會放在哪->->-> `Arguments放在FEC中的LexicalEnvironment區塊`


#🧠 在Function Execution Context 中的argument object 內容為何，通常會如何用？ ->->-> `本身會是想傳進函式的參數，並在執行階段時使用和存取`

#🧠 在Global Execution Context 中的global object在瀏覽器和Node.js分別成什麼？又會是什麼？ ->->-> `	- 瀏覽器：window物件來設定，其代表對應畫面的呈現元件 - Node.js：global 物件來設定，其代表執行環境本身`



#🧠 Function Execution Context的creation phase時機點為何？(ByteCode) ->->-> `在編譯時期先對所有EC準備建立EC所需的資料和對應的ByteCode後，並於執行之前先執行ByteCode來建立FEC`
<!--SR:!2023-09-19,236,249-->


#🧠 Function Execution Context 的 FEC範圍是？->->-> `以區塊內或者函式內的所有區域變數、函式為主、不包含內部額外的函式，不包含額外用區塊和函式包住的程式碼`
<!--SR:!2023-02-10,147,250-->


#🧠 Function Execution Context的creation phase 製作流程為何(提示：this物件、lexicalEnvironment、variableEnvironment、outer)->->-> `將呼叫的參數和引數以識別字來紀錄在LexicalEnvironment、建立this物件並決定this參照於誰、建立Arguments物件來儲存賦予對應函數的參數並放置FEC中的LexicalEnvironment區塊、掃描所有函式呼叫、const/let變數識別字並放入LexicalEnvironment區塊、掃描所有var變數識別字並放入VariableEnvironment區塊、設定outer。`
<!--SR:!2023-01-30,139,250-->


#🧠 Function Execution Context的creation phase：如何處理建立Arguments物件來儲存賦予對應函數的參數並放置FEC中的LexicalEnvironment區塊 以圖片為例子 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655278116/blog/javascript/lexical%20scope/function-execution-context-example_lnumes.png)(提示參數、參數長度) ->->-> `主要會包含參數、參數長度，以下面函式呼叫為例，當呼叫並執行test函式的第一段前會先建立對應的FEC，其中會先建立Arguments物件儲存1、3、4以及參數長度，其中0-2為代表著test呼叫中的argument1至argument3，而length則是代表著參數長度(如result那樣呈現)，而Arguments所儲存的變數皆為let類型的變數宣告，所以會將Arguments放在FEC中的LexicalEnvironment區塊`
<!--SR:!2023-01-27,137,250-->

#🧠 function Execution Context的creation phase：會如何處理函式、const/let變數、var變數(提示：分別放哪個EnvironmentRecords) ->->-> `從FEC收集函式宣告、let/const形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中、從GEC收集var形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中。`
<!--SR:!2023-03-21,159,230-->

#🧠 function Execution Context的creation phase ：outer 會指向什麼？->->-> `outer會是指向呼叫該EC的EC，也就是代表從全域呼叫的GlobalExectionContext或者代表從其他函式呼叫的EC`
<!--SR:!2023-04-20,193,250-->


#🧠 function Execution Context的execution phase ：會如何對context更新->->-> `建立完FEC後，JavaScript 引擎隨後就會在FEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context`
<!--SR:!2023-10-02,285,250-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[this]]
Links:
[[Global Execution Context 在creation phase建立對應GEC所擁有的environment record、this、outer，而在execution phase 是更新GEC內容(environment record)]]
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
[[當執行Bytecode來決定this binding時，若是遇到：非箭頭函式呼叫，就分別以new binding、implicit binding、explicit binding、default binding來決定他們函式呼叫時的this 是什麼；箭頭函式呼叫，就以語彙綁定]]
References:
