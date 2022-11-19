## 描述



[[@wikidataCallSiteRevision]]
> In programming, a spot of a function or subroutine is the location (line of code) where the function is called (or may be called, through dynamic dispatch). A call site is where zero or more arguments are passed to the function, and zero or more return values are received.

重點：
- call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置
- call site 用途：
	- 用來判斷目前執行環境的this 會是什麼之依據
- 用來判斷目前執行環境的this 會是什麼之依據
	- call site
	- call stack
### call site 案例
```
function baz() {
	console.log("baz");
	bar(); 
}

function bar() {
	console.log("bar");
	foo(); 
}

function foo() {
	console.log("foo");
}

baz(); 
```



```
function baz() {
	// stack: baz
	// 目前呼叫地點處於global scope
	console.log("baz");
	bar(); // bar 的呼叫地點
}

function bar() {
	// stack: baz->bar
	// 目前呼叫地點處於function baz scope
	console.log("bar");
	foo(); // foo 的呼叫地點
}

function foo() {
	// stack: baz->bar->foo
	// 目前呼叫地點處於function foo scope
	console.log("foo");
}

baz(); // baz 的呼叫地點
```



## 複習

#🧠 電腦科學裡的call site 是什麼？ ->->-> `call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置`
<!--SR:!2022-11-21,27,250-->

#🧠 電腦科學裡的call site 是指特定函式被呼叫的位置，其位置是什麼？->->-> `其位置會是指程式碼的位置`
<!--SR:!2023-01-28,70,250-->

#🧠 JS ： 用來判斷目前執行環境的this 會是什麼之依據 是哪些？->->-> `call site、call stack`
<!--SR:!2022-12-21,37,230-->

#🧠 call site在JS的用途是什麼？ ->->-> `判斷目前執行環境的this 會是什麼之依據 `
<!--SR:!2022-11-20,27,250-->

#🧠 請問baz、bar、foo的 call site和call stack是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665485554/blog/javascript/this-binding/call-site/call-site-example_nbpxxl.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665485840/blog/javascript/this-binding/call-site/call-site-example-answer_bujtbo.png)`
<!--SR:!2022-11-22,28,250-->

---
Status: #🌱 
Tags:
Links:
References:
[[@wikidataCallSiteRevision]]