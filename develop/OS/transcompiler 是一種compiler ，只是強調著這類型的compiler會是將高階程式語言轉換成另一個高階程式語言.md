## 描述



### 什麼是 transcompiler
[[@wikidataSourcetosourceCompiler2022]] 所描述：
> A source-to-source translator, source-to-source compiler (S2S compiler), transcompiler, or transpiler is a type of translator that takes the source code of a program written in a programming language as its input and produces an equivalent source code in the same or a different programming language. 


重點：
- transcompile 、source-to-source compiler (S2S compiler)
- transcompiler 也是一種compiler，只是強調著這類型compiler會將高階程式語言A轉換成另一種高階程式語言B
- 高階程式語言A和高階程式語言B可以分別定義為同種高階語言的不同版本、兩個不同高階語言


###  transcompiler vs. compiler 

[[@wikidataCompiler2022]] 所描述的compiler：
> a compiler is a computer program that translates computer code written in one programming language (the source language) into another language (the target language)
> 
> The name "compiler" is primarily used for programs that translate source code from a high-level programming language to a lower level language 

[[@wikidataSourcetosourceCompiler2022]] 所描述：
> A source-to-source translator converts between programming languages that operate at approximately the same level of abstraction, while a traditional compiler translates from a higher level programming language to a lower level programming language. 




重點：
- compiler 本身是程式，專門把特定程式語言轉換成另一個目標程式語言的程式，狹義上來說，會是從高階程式語言轉換成低階程式語言，高低階會是人類易讀性來區分，越高就容易讓人類理解，機器較不易理解；越低就容易讓機器理解，人類較不易理解
- transcompiler 和 compiler 差別是：
	- compiler 專門指高階語言轉換成低階語言
	- transcompiler 專門指高階語言轉換成另一個高階語言


### source code 是什麼？
[[@wikidataSourceCodeWikipedia]] 意思：
> In computing, source code is any collection of code, with or without comments, written using a human-readable programming language, usually as plain text. 

> Source code (also referred to as source or code) is the version of software as it is originally written (i.e., typed into a computer) by a human in plain text (i.e., human readable alphanumeric characters)

source
> the place something comes from or starts at, or the cause of something


重點：
- source code 的 source 是指起源、原始，code則是指程式碼，合在一起就是指程式碼的最原始形式或者最一開始的形式
- source code 泛指著程式碼被編譯前的形式，也就是高階程式語言。



## 複習
#🧠 source code 命名緣由？ ->->-> `source code 的 source 是指起源、原始，code則是指程式碼，合在一起就是指程式碼的最原始形式或者最一開始的形式`

#🧠 source code 是泛指什麼？ ->->-> `泛指著程式碼被編譯前的形式，也就是高階程式語言`

#🧠 compiler 較嚴格的定義是什麼？ ->->-> `compiler 本身是程式，專門把特定程式語言轉換成另一個目標程式語言的程式，狹義上來說，會是從高階程式語言轉換成低階程式語言`

#🧠 程式語言的高低階會是指什麼？ ->->-> `高低階會是人類易讀性來區分，越高就容易讓人類理解，機器較不易理解；越低就容易讓機器理解，人類較不易理解`

#🧠 compiler 較不嚴格的定義是什麼？  ->->-> `compiler 本身是程式，專門把特定程式語言轉換成另一個目標程式語言的程式`


#🧠 transcompiler 是什麼？ ->->-> `transcompiler 也是一種compiler，只是強調著這類型compiler會將高階程式語言A轉換成另一種高階程式語言B`

#🧠 transcompiler 是高階程式語言A轉換成另一種高階程式語言B的程式，那麼程式語言A和程式語言B具體可以是？->->-> `為同種高階語言的不同版本、兩個不同高階語言`

#🧠 compiler 和 transcompiler 之間的差別是什麼？ ->->-> `	- compiler 專門指高階語言轉換成低階語言 - transcompiler 專門指高階語言轉換成另一個高階語言`



---
Status: #🌱 
Tags:
[[Operating System]] - [[Compiler]]
Links:
References:
[[@wikidataSourcetosourceCompiler2022]]
[[@wikidataCompiler2022]]
[[@wikidataSourceCodeWikipedia]]