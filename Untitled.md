## GEC - creation phase

0. 這裡的概念以ECMA2015-ECMA2019為主。

1. 發生時間點：當引擎要開始執行某個檔案上的JS程式碼時，就會先建立GEC

2. GEC範圍：以檔案內的全域區塊為一個區塊(block)，不包含函式內部的執行、區塊內的另一個區塊的(Block)的內部執行

3. 製作流程：

- 建立一個全域物件：在瀏覽器會是名為window的全域物件，在Node.js會是名為global的全域變數

- 建立this物件並決定this參照於誰：在這裡建立完會去指向當前被建立的全域變數

- 建立Lexical Environment：主要分為LexicalEnvironment、VariablEenvironment，這兩者會包含Environment Records、Outer reference、Thisbinding這三種主要屬性(如下)，而EnvironmentRecord的Type可以定義為Declarative或者Object來決定EnvironmentRecord的類型是什麼，最後Lexical Environment主要定義該Execution Context能夠使用的識別名字是為何以及對應何種變數、函式，

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

在這裡由於只有函式宣告不受scope的影響，所以函式宣告部分能夠確定其對應內容，而const/let的變數宣告會受限於scope而無法馬上確定，因此對應let/const的變數宣告會是uninitialized來表示該變數還未宣告，接著Outer reference和ThisBinding會因為目前EC為GEC而分別設定為null和Global Object。

  

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

- VariablEenvironment：從GEC收集函式宣告、var形式的變數宣告並以下面形式來存放在EnvironmentRecord屬性中，

```

identifier: <var variable>

```

在這裡由於只有var變數本身沒有scope的概念，所以不受到scope的影響，因此對應var的變數值會是undefined代表已經宣告但只是還未指派任何初始值給予，接著Outer reference和ThisBinding會因為目前EC為GEC而分別設定為null和Global Object。

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

  

## GEC - execution phase

1. 建立完GEC後，JavaScript 引擎隨後就會在GEC的環境下一行又一行執行程式碼，並根據執行結果來更新Lexical Environment內某個特定名稱的對應值或者調用其他區塊或者其他函式，使其產生該區塊或者該函式的execution context

> JavaScript Engine executes the code line by line

2. 在這裏主要會做：

- 更新Lexical Environment的對應值