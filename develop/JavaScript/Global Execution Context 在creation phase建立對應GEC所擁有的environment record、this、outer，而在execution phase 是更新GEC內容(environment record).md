

## 描述

這裡的概念以ECMA2015-ECMA2019為主。
### GEC - creation phase
1.  發生時間點：當引擎要開始執行某個檔案上的JS程式碼時，就會先建立GEC
2. GEC範圍：以檔案內的全域區塊為一個區塊(block)，不包含函式內部的執行環境、也不包含區塊的執行環境

3. 製作流程：

- 建立一個全域物件：在瀏覽器會是名為window的全域物件，在Node.js會是名為global的全域物件
- 建立this物件並決定this參照於誰：在這裡建立完會去指向當前被建立的全域變數

- 建立Lexical Environment，主要分為：
	- LexicalEnvironment：包含Environment Records、Outer reference、Thisbinding這三種主要屬性
	- VariablEenvironment：包含Environment Records、Outer reference、Thisbinding這三種主要屬性 
	- EnvironmentRecord的Type可以定義為Declarative或者Object來決定EnvironmentRecord的類型是什麼，最後Lexical Environment主要定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式，

```

GlobalExectionContext = {
	LexicalEnvironment: {
		EnvironmentRecord: {
			Type: "Declarative" | "Object"
			// Identifier bindings go here
		}

		outer: <null>,
		ThisBinding: <Global Object>
	},

	VariableEnvironment: {
		EnvironmentRecord: {
			Type: "Declarative" | "Object"
			// Identifier bindings go here
		}

		outer: <null>,
		ThisBinding: <Global Object>
	}
}

```

- LexicalEnvironment 從GEC收集函式宣告、let/const形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中，

```

identifier: <function>
identifier: <const variable>
identifier: <let variable>
```

在這裡由於函式宣告本身是有scope概念，只是在GEC和FEC的creation phase期間由於一開始可以直接用函式物件來設定函式識別字所對應的內容，所以才能不在execution phase定義其內容；而const/let的變數宣告會受限於擁有scope概念而且一開始是呈現沒任何記憶體分配且沒設定初始值，因此對應let/const的變數宣告會是uninitialized來表示該變數還沒有任何記憶體分配以及未指定初始值

```
GlobalExectionContext = {
	LexicalEnvironment: {
		EnvironmentRecord: {
			Type: "Declarative",
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

在這裡由於只有var變數本身由於沒有scope的概念，所以能夠先分配記憶體給該變數以及預設初始值-undefined，因此對應var的變數值會是undefined代表已經宣告但只是還沒有除了預設指派以外的手段來給予任何初始值給予，接著Outer reference和ThisBinding會因為目前EC為GEC而分別設定為null和Global Object。

```
GlobalExectionContext = {
	VariableEnvironment: {
		EnvironmentRecord: {
			// Identifier bindings go here
			identifier1: undefined
		}

		outer: <null>,
		ThisBinding: <Global Object>
	}
}
```

- 補充資訊：Outer reference是用來實現scope chain，當目前EC找不到對應名稱時就會往outer所指向的EC來尋找，而ThisBinding則是指定This變數要指定哪個對象。

 
4. 最終結果會是如下：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1646750816/backend/lexical%20environment/GlobalExecContext_ylw8a9.png)

#### scope 概念代表著什麼？
若一個變數具有scope概念，代表該變數是具有一定程度的識別空間、定義該變數何時分配記憶體、內容指派、記憶體釋放

反之，若沒有scope概念的話，就代表著該變數從一開始的執行就已經以整個檔案作為識別空間，並且一開始就分配記憶體並先設定初始值為undefined、內容指派，並於檔案執行結束後釋放其記憶體位置

#### function 宣告本身是有scope概念嗎？
答案是有的，在這裡舉一個例子：這裡有兩個函式-testFunction1和testFunction2，而前者是放在全域，後者是放在testFunction1內，若function宣告本身是沒有scope概念的話，那麼就能在全域環境下呼叫到原本只能在testFunction1呼叫得到的testFunction2

```
function testFunction1() {
	console.log('test func1')
	function testFunction2() {
		console.log('test func2')
	}
}
testFunction1()
testFunction2()
```

結果是：
```
test func1
ReferenceError: testFunction2 is not defined
```

若改在testFunction1呼叫testFunction2的話，
```
function testFunction1() {
	console.log('test func1')
	function testFunction2() {
		console.log('test func2')
	}
	testFunction2()
}
testFunction1()
```

就會是
```
test func1
test func2
```
證明函式宣告本身是有scope概念，只是在GEC和FEC的creation phase期間由於一開始可以直接用函式物件來設定函式識別字所對應的內容，所以才能不在execution phase定義其內容
#### Outer reference 是什麼？
1. Outer reference是用來實現scope chain，當目前EC找不到對應名稱時就會往outer所指向的EC來尋找
2. Outer reference通常會是指向建立目前EC的EC


#### ThisBinding 是什麼？
1. ThisBinding則是指定This變數要指定哪個對象。
2. 在Global Execution Context會指向該環境下的特有全域物件 ，比如在瀏覽器就是window這全域物件 ，在Node.js會是名為global的全域物件

### GEC - execution phase
1. 建立完GEC後，JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context

> JavaScript Engine executes the code line by line

2. 在這裏主要會做：
- 更新Lexical Environment的對應值


## 複習

#🧠  JavaScript： 一個變數擁有scope概念就代表著？(提示：識別、何時記憶體分配、指派、釋放)->->-> `若一個變數具有scope概念，代表該變數是具有一定程度的識別空間、定義該變數何時分配記憶體、內容指派、記憶體釋放`

#🧠  JavaScript： 一個變數沒擁有scope概念就代表著？(提示：識別、何時記憶體分配、指派、釋放)->->-> `反之，若沒有scope概念的話，就代表著該變數從一開始的執行就已經以整個檔案作為識別空間，並且一開始就分配記憶體並先設定初始值為undefined、內容指派，並於檔案執行結束後釋放其記憶體位置`

#🧠 GEC - creation phase 的發生時機點->->-> `當引擎要開始執行某個檔案上的JS程式碼時，就會先建立GEC`

#🧠 GEC - creation phase 的範疇是哪些？ ->->-> `以檔案內的全域區塊為一個區塊(block)，不包含函式內部的執行環境、也不包含區塊的執行環境`

#🧠 GEC - creation phase 的製作流程是哪些(提示：先從建立GEC這物件說起，全域變數、this變數、建立所謂的Lexical Environment)->->-> `建立一個全域物件：在瀏覽器會是名為window的全域物件，在Node.js會是名為global的全域變數、建立this物件並決定this參照於誰：在這裡建立完會去指向當前被建立的全域變數、建立Lexical Environment`

#🧠 Global Execution Context 在Creation phase遇上函式時，會設定識別字以及對應的函式嗎？ ->->-> `在這裡由於函式宣告本身是有scope概念，只是在GEC和FEC的creation phase期間由於一開始可以直接用函式物件來設定函式識別字所對應的內容，所以才能不在execution phase定義其內容`

#🧠 Global Execution Context 在Creation phase遇上const/let變數時，會設定識別字以及對應的變數嗎？(提示：scope、沒記憶體分配、初始值) ->->-> `const/let的變數宣告會受限於擁有scope概念而且一開始是呈現沒任何記憶體分配且沒設定初始值，因此對應let/const的變數宣告會是uninitialized來表示該變數還沒有任何記憶體分配以及未指定初始值`

#🧠Global Execution Context 在Creation phase遇上var變數時，會設定識別字以及對應的變數嗎->->-> `只有var變數本身由於沒有scope的概念，所以能夠先分配記憶體給該變數以及預設初始值-undefined，因此對應var的變數值會是undefined代表已經宣告但只是還沒有除了預設指派以外的手段來給予任何初始值給予`


#🧠 Global Execution Context 的Lexical Environment 分為哪兩個？->->-> ` LexicalEnvironment、VariablEenvironment，這些都含有Environment Records、Outer reference、Thisbinding`


#🧠 Global Execution Context ： LexicalEnvironment 和VariablEenvironment 物件各有什麼樣屬性 ？->->-> ` EnvironmentRecord、outer、ThisBinding`

#🧠 Global Execution Context ：LexicalEnvironment 主要記錄著什麼？ ->->-> ` LexicalEnvironment 從GEC收集函式宣告、let/const形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中

#🧠 Global Execution Context ：VariablEenvironment 主要記錄著什麼？ ->->-> `從GEC收集var形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中`


#🧠 Global Execution Context ：Lexical Environment 中的Environment Records 是什麼(在Creation phase和Execution phase) ->->-> `一開始在Creation 階段中，EnvironmentRecord的Type可以定義為Declarative或者Object來決定EnvironmentRecord的類型是什麼，最後Lexical Environment主要定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式，在Execution 階段中，會是JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context`

#🧠 Global Execution Context  (Creation phase)：Lexical Environment 中的Environment Records 會有什麼樣的變化(提示：建立)  ->->-> `定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式`

#🧠 Global Execution Context  (Execution phase)：Lexical Environment 中的Environment Records 會有什麼樣的變化(提示：更新) ->->-> `建立完GEC後，JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context`



#🧠 Global Execution Context ：Lexical Environment 中的Outer reference 是什麼？ 做什麼用？->->-> `Outer reference是用來實現scope chain，當目前EC找不到對應名稱時就會往outer所指向的EC來尋找，主要會指向呼叫建立目前EC的EC，比如GEC呼叫一個函式，那麼其函式的FEC之outer就會是指向於呼叫FEC的GEC`

#🧠 Global Execution Context ：Lexical Environment 中的ThisBinding 是什麼？ 做什麼用？那麼指向什麼? (提示：以瀏覽器或者Node.js來說明)->->-> `指定This變數要指定哪個對象，在GEC的話會是指向於GEC特有的全域物件，比如在瀏覽器就是名為window的全域物件，在Node.js就中就是名為global的全域變數`


#🧠  若於Global Execution Context的建立期間遇到函式、變數的話，其對應識別字會是如何？對應內容是否能有值？(提示：函式不受scope影響，變數會->->-> `在這裡由於只有函式宣告本身可以透過函式名稱來呼叫，所以不受到對應值無法確定的問題，而const/let的變數宣告會受限於對應值無法確定的問題，因此對應let/const的變數宣告會是uninitialized來表示該變數還未宣告`

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
References: