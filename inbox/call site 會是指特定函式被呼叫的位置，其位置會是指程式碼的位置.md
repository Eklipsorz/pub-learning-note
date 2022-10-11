## 描述



[[@wikidataCallSiteRevision]]
> In programming, a spot of a function or subroutine is the location (line of code) where the function is called (or may be called, through dynamic dispatch). A call site is where zero or more arguments are passed to the function, and zero or more return values are received.

重點：
- call site 會是指特定函式被呼叫的位置，其位置會是指程式碼的位置
- call site 用途：
	- 用來判斷目前執行環境的this 會是什麼之依據

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

#🧠 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665485554/blog/javascript/this-binding/call-site/call-site-example_nbpxxl.png) ->->-> ``

#🧠 Question :: ->->-> ``


---
Status: #🌱 
Tags:
Links:
References:
[[@wikidataCallSiteRevision]]