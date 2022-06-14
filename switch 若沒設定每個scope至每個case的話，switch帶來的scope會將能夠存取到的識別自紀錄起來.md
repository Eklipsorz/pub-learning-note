
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

### 總結：

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[Scope 是指某識別字對應特定實體的合法使用範圍，具體實現Scope的方式有Lexical Scope 和Dynam Scope]]
References:
[[@tengxunivwebtuanduiJieJueUnexpectedLexical]]



