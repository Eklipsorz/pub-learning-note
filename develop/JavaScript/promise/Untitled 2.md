## 描述


### 背景


- promise 本身是一個概念，具體實現會有以下幾個版本的promise實作，甚至有不支援promise的瀏覽器
	1. 特定瀏覽器所提供的promise
	2. 特定函式庫所提供的promise
	3. ES6 官方提供的promise

基於以上這點，會在實作上由於實作版本內容不一，而很難判別誰到底是promise


### thenable duck typing

解法為
1. 使用duck typing概念來判別
[[duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別]]


能夠擁有then方法的任何物件或者函式，稱之為thenable，換言之，就是可以用promise規範中的then形式來執行



## 複習

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別]]
References: