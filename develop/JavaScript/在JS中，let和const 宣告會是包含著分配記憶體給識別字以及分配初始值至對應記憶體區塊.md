## 描述

[[@ReferenceErrorCanAccess]] ：
> ReferenceError: can't access lexical declaration 'X' before initialization

> The JavaScript exception "can't access lexical declaration 'variable' before initialization" occurs when a lexical variable was accessed before it was initialized. This happens within any block statement, when let or const variables are accessed before the line in which they are declared is executed.

重點：
- 在JS中，let/const 宣告會是以下動作，且不可分割的
	- 分配記憶體給對應識別字
	- 分配初始值至對應記憶體區塊
- 若顯示以下訊息，代表著識別字X的宣告還未做完就先存取其識別字對應的記憶體區塊內容

```
ReferenceError: can't access lexical declaration 'X' before initialization
```


## 複習
#🧠 在JS中，let/const 宣告會是包含哪些動作？ ->->-> `分配記憶體給對應識別字、分配初始值至對應記憶體區塊`

#🧠 在JS中，顯示以下訊息 ReferenceError: can't access lexical declaration 'X' before initialization 這代表著什麼？ ->->-> `代表著識別字X的宣告還未做完就先存取其識別字對應的記憶體區塊內容`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@ReferenceErrorCanAccess]]