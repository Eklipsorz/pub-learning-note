> JavaScript **Hoisting** refers to the process whereby the interpreter appears to move the _declaration_of functions, variables or classes to the top of their scope, prior to execution of the code.

> Hoisting allows functions to be safely used in code before they are declared.

> Variable and class _declarations_ are also hoisted, so they too can be referenced before they are declared. Note that doing so can lead to unexpected errors, and is not generally recommended.



> 提升（Hoisting）是在 ECMAScript® 2015 Language Specification 裡面找不到的專有名詞。它是一種釐清 JaveScript 在執行階段內文如何運行的思路（尤其是在創建和執行階段）。然而，提升一詞可能會引起誤解：例如，提升看起來是單純地將變數和函式宣告，移動到程式的區塊頂端，然而並非如此。變數和函數的宣告會在編譯階段就被放入記憶體，但實際位置和程式碼中完全一樣。


### 範例
在執行任何程式碼前，JavaScript 會把函式宣告放進記憶體裡面，這樣做的優點是：可以在程式碼宣告該函式之前使用它。 例如：

```
function catName(name) {
  console.log("My cat's name is " + name);
}

catName("Tigger");
/*
上面程式的結果是: "My cat's name is Tigger"
*/
```

## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: