
## 描述
引用[[@tengxunivwebtuanduiJieJueUnexpectedLexical]]所描述的：

問題源自於ESLINT給予的警告
```
Unexpected lexical declaration in case block(no-case-declarations)
```


### 異常現象1

```
const result = 2

switch (result) {
	case 1:
		let foo = 1
		break
	
	case 2:
		console.log(foo)
		break
}

```

當如果執行這段的話，會跑出系統找到識別字但卻還沒有初始化的訊息：
```
ReferenceError: Cannot access 'foo' before initialization
```

而不是跑出找不到對應識別字：
```
ReferenceError: foo is not defined
```

### 異常現象2

  
```
const result = 2

switch (result) {

	case 1:
		function testConsole() { console.log('hihi') }
		break
		
	case 2:
		testConsole()
		break
}
```

當如果執行的話，會成功跑出
```
hihi
```

而不是跑出找不到對應識別字：
```
ReferenceError: testConsole is not defined
```

### 若改給每個case一個Execution context的話

```
const result = 2

switch (result) {
	case 1: {
		let foo = 1
		break
	}
	
	case 2: {
		console.log(foo)
		break
	}
}
```

透過{}來給定每個case一個Execution context，這使得switch的execution context無法識別，進而讓程式執行的時候，跑出找不到識別字
```
ReferenceError: foo is not defined
```


換成案例2的話
```
const result = 2

switch (result) {

	case 1: {
		function testConsole() { console.log('hihi') }
		break
	}
		
	case 2: {
		testConsole()
		break
	}
}
```

執行後會得到以下結果，其中testConsole會是underfined，這說明還是能夠在其他execution context找到對應識別字，只是找不到實際的值，這部分仍須待查
```
TypeError: testConsole is not a function
```

### 總結：
1. switch 本身的execution context是由{}來決定，無論其內容是什麼，只要內容不是被額外的execution context包住，都會被識別出來
```
switch (...) {

..
}
```
2. 面對這問題，若考量到每個case的變數都要有獨立的scope，那麼就設定{}來建立每個case的execution context
```
switch (..) {

	case 1: {
		....
	}
	
	case 2: {
		....
	}
}
```

## 複習
#🧠 請問這段JavaScript程式碼若被執行的話，會得到什麼? 說明為什麼會這樣？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655193210/blog/javascript/lexical%20scope/switch-lexcial-scope-1_rryoim.png) ->->-> `會跑出系統找到識別字但卻還沒有初始化的訊息，這是因爲switch 的execution context會以{}為主來識別他擁有的識別字，其中會包含foo，所以只要在switch內的context執行就會找到該識別字`
<!--SR:!2024-03-27,240,230-->

#🧠  請問這段JavaScript程式碼若被執行的話，會得到什麼? 說明為什麼會這樣![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655193339/blog/javascript/lexical%20scope/switch-lexcial-scope-2_wpzxli.png)->->-> `hihi，這是因爲switch 的execution context會以{}為主來識別他擁有的識別字，其中會包含testConsole，所以只要在switch內的context執行就會找到該識別字`
<!--SR:!2025-07-14,676,250-->


#🧠 JavaScript：若不想讓每個case都能存取其他case的識別字，該如何做？(提示：也建立環境吧) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655193210/blog/javascript/lexical%20scope/switch-lexcial-scope-1_rryoim.png) 和  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655193339/blog/javascript/lexical%20scope/switch-lexcial-scope-2_wpzxli.png)->->-> `替每個case增加execution context，也就是用{}`
<!--SR:!2024-07-04,454,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[Scope 是指某識別字對應特定實體的合法使用範圍，具體實現Scope的方式有Lexical Scope 和Dynam Scope]]
References:
[[@tengxunivwebtuanduiJieJueUnexpectedLexical]]



