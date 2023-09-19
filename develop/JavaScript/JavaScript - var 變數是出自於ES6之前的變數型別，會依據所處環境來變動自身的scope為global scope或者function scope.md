

## 描述
JavaScript - var 變數本身沒scope概念，所以當在檔案全域宣告就於檔案的一開始就分配記憶體，而當在函式宣告就等於在函式一開始分配記憶體

[[@ithomeBianShuJiChu]] 所描述：
> ## var變數的有效範圍
> 有效範圍講的專業一點叫`作用域(scope)`，var變數是遵照 `function scope`。
> ### 甚麼是「var變數遵照 `function scope`」
> 講人話就是：`var`關鍵字令出的變數，他的有效範圍以`function`界定。


[[@chengshimanongJSXuanGaoBianShuVar]]

> 在 ES6 前，並沒有區塊作用域（block scope）的概念，僅有全域（global scope）與函式作用域（function scope），所以 `var` 宣告的變數，具有函式作用域（function scope）的性質，代表**切分最小單位的有效範圍是 function**。

> 直到 ES6 後，新增區塊切分的概念， `let / const` 宣告的變數，才具有區塊作用域（block scope）的性質，**切分最小單位的有效範圍是 blcok**。

重點：
- ES6 前是沒有block scope，只有global scope 概念和function scope 概念
- var 變數本身出自於ES6之前的語法，所以其作用域會依據變數所處的環境來決定自己是global scope ? 還是function scope
- let/const 是出自於ES6，所以會有block scope、function scope、global scope，且最小scope單位是block scope
### var 變數若放在block scope的話
var 變數由於是出自於只有global scope和function scope的ES6以前版本，若遇到ES6出現的block scope，會直接忽視block scope，並且依據其block scope原本處於的scope是否為function scope來決定自己的scope是否為function scope

比如說var 被放置block scope
```
function xxx() {
	{
		{
			var x = 100
		}
	}
}
```
，但系統會這樣子看待x變數：直接忽視block scope，並決定其var變數為function scope
```
function xxx() {

	var x = 100
	
}
```

### var 變數若處於function scope
var 變數只會在該函式能夠被識別，並且當執行到該函式之前，系統會先賦予記憶體空間以及初始值undefined給定所有處在function的var變數，直到正式執行時，就更改其內容，最後執行到函式要結束時，就會釋放var變數的記憶體

###  var 變數若處於global scope 

 var變數會變成整個檔案都能夠被識別，並且當JS核心執行之前就會先賦予記憶體空間以及初始值undefined給定所有處在全域的var變數，直到正式執行時，就會更改其內容，最後執行到檔案要結束執行，就會釋放var變數的記憶體
 


#### 舉例1：在檔案全域下宣告var

當執行檔案的全域前，會先分配記憶體空間給var變數，並設置預設初始值-undefined，在這會是設定test為undefined，隨後正式執行後，就按照test = a 來指派其變數
```
var test = a

function xxx() {

}

console.log(test)
```

在全域宣告的var變數會以整個檔案的全域作為scope來分配記憶體、初始值分配、釋放記憶體

#### 舉例2：在函式下宣告var

當改在函式內宣告var變數時，並想在全域下印出其值

```
function xxx() {
	var test = a
}

console.log(test)
```
那麼會獲取以下錯誤訊息，來表示他們找不到var變數-test
```
ReferenceError: test is not defined
```

可若是將function改成多層{}的話，卻可以印出'hi'

```
{	
	{
		var test = 'hi'
	}
}

console.log(test)
```

從這裡可以得知var變數只會生效於函式，並以函式當作另一個檔案的全域來存活，當函式要呼叫之前，就分配記憶體給test、分配初始值undefined給test、在函式結束後釋放記憶體
```
function xxx() {
	var test = a
}
```

## 複習
#🧠 在ES6之前的scope是有哪些種類(提示：全x、函x)->->-> `只有global scope、function scope`
<!--SR:!2024-07-25,468,250-->

#🧠  var 變數有沒有scope 概念？ 具體來說是什麼？ 它出自於ES6? ES6以前？->->-> `var變數是有的，具體來說它出自於只有global scope、function scope的ES6以前版本，而var變數的scope本身會依賴著自己所處的環境是不是函式而決定是否為function scope？還是global scope`
<!--SR:!2024-03-08,382,250-->

#🧠  var 變數若處於function scope，這說明什麼？(提示：識別、記憶體、初始值、釋放) ->->-> `var 變數只會在該函式能夠被識別，並且當執行到該函式之前，系統會先賦予記憶體空間以及初始值undefined給定所有處在function的var變數，直到正式執行時，就更改其內容，最後執行到函式要結束時，就會釋放var變數的記憶體`
<!--SR:!2024-08-26,489,250-->

#🧠  var 變數若處於global scope，這說明什麼？(提示：識別、記憶體、初始值、釋放) ->->->  `var變數會變成整個檔案都能夠被識別，並且當JS核心執行之前就會先賦予記憶體空間以及初始值undefined給定所有處在全域的var變數，直到正式執行時，就會更改其內容，最後執行到檔案要結束執行，就會釋放var變數的記憶體`
<!--SR:!2024-01-10,113,210-->

#🧠 var 變數若放在block scope的話，系統會如何決定var變數的scope ->->-> `var 變數由於是出自於只有global scope和function scope的ES6以前版本，若遇到ES6出現的block scope，會直接忽視block scope，並且依據其block scope原本處於的scope是否為function scope來決定自己的scope是否為function scope`
<!--SR:!2023-12-01,128,210-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@chengshimanongJSXuanGaoBianShuVar]]
[[@ithomeBianShuJiChu]]