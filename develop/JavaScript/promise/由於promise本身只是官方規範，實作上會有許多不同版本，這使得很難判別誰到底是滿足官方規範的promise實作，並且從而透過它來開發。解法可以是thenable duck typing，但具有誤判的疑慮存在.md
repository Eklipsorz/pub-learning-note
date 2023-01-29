## 描述


### 背景


- promise 本身是一個概念，具體實現會有以下幾個版本的promise實作，甚至有不支援promise的瀏覽器
	1. 特定瀏覽器所提供的promise
	2. 特定函式庫所提供的promise
	3. ES6 官方提供的promise

基於以上這點，會在實作上由於實作版本內容不一，而很難判別誰到底是滿足官方規範的promise實作，並且從而透過它來開發。


若貿然不管，無法確保promise在執行上是按照ES6 官方規範下的promise




### thenable duck typing

解法範例為
1. 使用duck typing概念來判別，比如說：
	- 判別特定物件是否為object或者function
	- 檢測特定物件是否擁有function型別的then 方法
[[duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別]]
```
if (
	p !== null && 
	(
		typeof p === "object" ||
		typeof p === "function"
	) &&
	typeof p.then === "function"
) {
	// 假設為thenable
} else {
	// 假設不為thenable
}
```
2. anti-branding
3. branding
但問題
1. 很容易被其他具有then方法但卻不是promise的物件給誤判


### thenable 定義

能夠擁有then方法的任何物件或者函式，且then必須是滿足promise規範，而這樣可稱之為thenable

## 複習

#🧠 thenable 定義為何？ ->->-> `能夠擁有then方法的任何物件或者函式，且then必須是滿足promise規範，而這樣可稱之為thenable`
<!--SR:!2023-01-29,3,250-->

#🧠 JS 的 promise 會是統一的版本嗎？為什麼？->->-> `並不是， promise 本身是一個概念，具體實現會有以下幾個版本的promise實作，甚至有不支援promise的瀏覽器：1. 特定瀏覽器所提供的promise 2. 特定函式庫所提供的promise 3. ES6 官方提供的promise`
<!--SR:!2023-02-08,10,250-->

#🧠 JS 的 promise 在實作上有何版本，若有沒有支援也請說出 ->->-> `1. 特定瀏覽器所提供的promise 2. 特定函式庫所提供的promise 3. ES6 官方提供的promise 4. 沒有支援任何promise實作的瀏覽器`
<!--SR:!2023-02-06,8,250-->



#🧠 JS 的 promise 在實作上是充斥著不同的版本，那會有什麼問題 ->->-> `若貿然不管，無法確保promise在執行上是按照ES6 官方規範下的promise`
<!--SR:!2023-02-05,7,250-->

#🧠 JS 的 promise 在實作上是充斥著不同的版本，若貿然不管，無法確保promise在執行上是按照ES6 官方規範下的promise，可以使用什麼解法，舉例->->-> `thenable duck typing，	- 判別特定物件是否為object或者function - 檢測特定物件是否擁有function型別的then 方法`
<!--SR:!2023-02-08,10,250-->

#🧠 JS 的 promise 在實作上是充斥著不同的版本，若貿然不管，無法確保promise在執行上是按照ES6 官方規範下的promise，可以使用什麼解法，再進一步假設解法為thenable duck typing，會是完善的嗎？為什麼？ ->->-> `並不完善，原因為很容易被其他具有then方法但卻不是promise的物件給誤判
<!--SR:!2023-02-06,8,250-->
`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別]]
References: