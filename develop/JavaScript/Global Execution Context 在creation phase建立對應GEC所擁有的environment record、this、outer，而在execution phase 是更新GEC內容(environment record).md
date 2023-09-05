

## 描述

這裡的概念以ECMA2015-ECMA2019為主。
### GEC - creation phase
1.  發生時間點：在編譯時期先對所有EC準備建立EC所需的資料和對應ByteCode後，並於執行之前先執行對應ByteCode建立GEC
2. GEC範圍：檔案裡的最外圍scope
3. 製作流程：

- 建立一個全域物件：在瀏覽器會是名為window的全域物件，在Node.js會是名為global的全域物件
- 建立this物件並決定this參照於誰：在這裡建立完會去指向當前被建立的全域物件

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

在這裡由於函式宣告具有以下特性
[[JavaScript：函式宣告本身就是識別字去對應一塊儲存函式內容的物件，所以在執行之前的掃描就可以以識別字去對應其函式，且初始值會是其函式內容]]
在GEC和FEC的creation phase期間由於一開始可以直接用識別字對應的物件，其物件的初始值會是函式內容本身；而const/let的變數宣告會受限於擁有scope概念，必須執行到對應scope才能有記憶體分配且並設定初始值，因此對應let/const的識別字對應物件之初始值會設定成uninitialized來表示該變數還沒有任何記憶體分配以及未指定初始值

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

在這裡由於只有var變數本身由於出自於只有global scope和function scope的ES版本的概念，var變數會依據自己所在是不是函式來決定是否為scope，

[[JavaScript - var 變數是出自於ES6之前的變數型別，會依據所處環境來變動自身的scope為global scope或者function scope]]


在這會是global scope，並且能夠按照特性先分配記憶體和設定初始值-undefined給定var變數，因此對應var的變數值會是undefined代表已經宣告但只是還沒有除了預設指派以外的手段來給予任何初始值給予，接著Outer reference和ThisBinding會因為目前EC為GEC而分別設定為null和Global Object。

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


#### lexical environment是什麼？
[[@manishkumarWhatLexicalEnvironmenta]] 所描述的
> A lexical environment is **a data structure that holds identifier-variable mapping**. (here identifier refers to the name of variables/functions, and the variable is the reference to actual object

重點：
- lexical environment 是一種資料結構，主要儲存每個識別字對應的物件是什麼、識別空間、記憶體位置
-  Global Execution Context 的Lexical Environment  和LexicalEnvironment/VariableEnvironment 有何關係？
	-  tLexical Environment本身是種資料結構，是在儲存每個識別字對應的物件是什麼以及識別空間，而LexicalEnvironment/VariableEnvironment 只是前者所包含的內容

#### scope 概念代表著什麼？
若一個變數具有scope概念，代表該變數是具有一定程度的識別空間、定義該變數何時分配記憶體、內容指派、記憶體釋放


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
<!--SR:!2024-02-09,365,250-->


#🧠 GEC - creation phase 的發生時機點->->-> `在編譯時期先對所有EC準備建立EC所需的資料和對應ByteCode後，並於執行之前先執行對應ByteCode建立GEC`
<!--SR:!2023-09-30,241,247-->


#🧠 GEC (Global Execution Context) 的紀錄範疇是哪些？ ->->-> `檔案裡的最外圍scope`
<!--SR:!2025-04-04,613,248-->

#🧠 GEC - creation phase 的製作流程是哪些(提示：先從建立GEC這物件說起，全域物件、this變數、建立所謂的Lexical Environment)->->-> `建立一個全域物件：在瀏覽器會是名為window的全域物件，在Node.js會是名為global的全域物件、建立this物件並決定this參照於誰：在這裡建立完會去指向當前被建立的全域物件、建立Lexical Environment`
<!--SR:!2023-09-28,283,250-->

#🧠 Global Execution Context 在Creation phase遇上函式時，會設定識別字以及對應的函式嗎？ ->->-> `在這裡由於函式宣告具有以下特性**JavaScript：函式宣告本身就是識別字去對應一塊儲存函式內容的物件，所以在執行之前的掃描就可以以識別字去對應其函式，且初始值會是其函式內容** 在GEC和FEC的creation phase期間由於一開始可以直接用識別字對應的物件，其物件的初始值會是函式內容本身`
<!--SR:!2025-03-07,590,248-->



#🧠 Global Execution Context 在Creation phase遇上const/let變數時，會設定識別字以及對應的變數嗎？(提示：scope、沒記憶體分配、初始值) ->->-> `const/let的變數宣告會受限於擁有scope概念，必須執行到對應scope才能有記憶體分配且並設定初始值，因此對應let/const的識別字對應物件之初始值會設定成uninitialized來表示該變數還沒有任何記憶體分配以及未指定初始值`
<!--SR:!2025-01-21,567,248-->


#🧠 Global Execution Context 在Creation phase遇上var變數時，會設定識別字以及對應的變數嗎->->-> `在這裡由於只有var變數本身由於出自於只有global scope和function scope的ES版本的概念，var變數會依據自己所在是不是函式來決定是否為scope，在這會是global scope，並且能夠按照特性先分配記憶體和設定初始值-undefined給定var變數，因此對應var的變數值會是undefined代表已經宣告但只是還沒有除了預設指派以外的手段來給予任何初始值給予`
<!--SR:!2025-05-30,645,248-->


#🧠 Global Execution Context 的Lexical Environment 分為哪兩個？(提示：紀錄種類，哪個紀錄const？哪個紀錄var)->->-> ` LexicalEnvironment、VariablEenvironment，這些都含有Environment Records、Outer reference、Thisbinding`
<!--SR:!2025-05-04,630,248-->

#🧠 JavaScript 的Lexical Environment  和LexicalEnvironment/VariableEnvironment 有何關係？(提示：請以資料結構來看待Lexical Environment)->->-> `Lexical Environment本身是種資料結構，是在儲存每個識別字對應的物件是什麼以及識別空間，而LexicalEnvironment/VariableEnvironment 只是前者所包含的內容`
<!--SR:!2023-09-13,50,188-->

#🧠 JavaScript Lexical Environment  是什麼？ ->->-> `Lexical Environment本身是種資料結構，是在儲存每個識別字對應的物件是什麼以及識別空間`
<!--SR:!2024-09-30,504,248-->

#🧠  JavaScript : 請用物件的形式來表達Execution Context 和 Lexical Environment的結構  ->->-> ``
<!--SR:!2023-10-12,44,245-->


#🧠 Global Execution Context ： LexicalEnvironment 和VariableEenvironment 物件各有什麼樣屬性 ？->->-> ` EnvironmentRecord、outer、ThisBinding`
<!--SR:!2023-11-02,57,208-->

#🧠 Global Execution Context ：LexicalEnvironment 主要記錄著什麼？ ->->-> ` LexicalEnvironment 從GEC收集函式宣告、let/const形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中
<!--SR:!2025-03-15,593,248-->

#🧠 Global Execution Context ：VariablEenvironment 主要記錄著什麼？ ->->-> `從GEC收集var形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中`
<!--SR:!2025-01-12,559,248-->


#🧠 Global Execution Context ：Lexical Environment 中的Environment Records 是什麼(在Creation phase和Execution phase) ->->-> `一開始在Creation 階段中，EnvironmentRecord的Type可以定義為Declarative或者Object來決定EnvironmentRecord的類型是什麼，最後Lexical Environment主要定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式，在Execution 階段中，會是JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context`
<!--SR:!2024-02-23,238,230-->

#🧠 Global Execution Context  (Creation phase)：Lexical Environment 中的Environment Records在建立時期當下 會有什麼樣的變化  ->->-> `定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式`
<!--SR:!2024-07-15,463,250-->

#🧠 Global Execution Context  (Execution phase)：Lexical Environment 中的Environment Records 在建立時期後會有什麼樣的變化 ->->-> `建立完GEC後，JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context`
<!--SR:!2025-03-10,594,248-->



#🧠 Global Execution Context ：Lexical Environment 中的Outer reference 是什麼？ 做什麼用？->->-> `Outer reference是用來實現scope chain，當目前EC找不到對應名稱時就會往outer所指向的EC來尋找，主要會指向呼叫建立目前EC的EC，比如GEC呼叫一個函式，那麼其函式的FEC之outer就會是指向於呼叫FEC的GEC`
<!--SR:!2025-03-31,609,248-->

#🧠 Global Execution Context ：Lexical Environment 中的ThisBinding 是什麼？ 做什麼用？那麼指向什麼? (提示：以瀏覽器或者Node.js來說明)->->-> `指定This變數要指定哪個對象，在GEC的話會是指向於GEC特有的全域物件，比如在瀏覽器就是名為window的全域物件，在Node.js就中就是名為global的全域物件`
<!--SR:!2025-02-28,584,248-->


#🧠  若於Global Execution Context的建立期間遇到函式、變數的話，其對應識別字會是如何？對應內容是否能有值？(提示：函式不受scope影響，變數會->->-> `在這裡由於只有函式宣告本身可以透過函式名稱來呼叫，所以不受到對應值無法確定的問題，而const/let的變數宣告會受限於對應值無法確定的問題，因此對應let/const的變數宣告會是uninitialized來表示該變數還未宣告`
<!--SR:!2023-12-04,280,248-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
[[JavaScript：函式宣告本身就是識別字去對應一塊儲存函式內容的物件，所以在執行之前的掃描就可以以識別字去對應其函式，且初始值會是其函式內容]]
[[JavaScript - var 變數是出自於ES6之前的變數型別，會依據所處環境來變動自身的scope為global scope或者function scope]]
References:
[[@manishkumarWhatLexicalEnvironmenta]]
