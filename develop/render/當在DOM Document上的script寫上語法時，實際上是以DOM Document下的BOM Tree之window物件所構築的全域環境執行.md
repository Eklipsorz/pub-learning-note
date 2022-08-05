

## 描述

> 在上面的內容有提到說，瀏覽器物件模型有著階層性的架構，最上層便是Window物件，代表著瀏覽器視窗本身，若是視窗中含有框架，則每個框架都還有屬於自己的window物件。

> 所有的BOM都可透過window來存取。window物件的使用不須經過宣告，可以直接使用。事實上，在Javcascript中，所有的全域變數、函式、物件，其實都是屬於window物件。舉例來說：

```
<script>
x=5;
alert (window.x); //輸出 5
</script>
```

重點：
- 當在DOM Document上的script寫上語法時，實際上是以DOM Document下的BOM Tree之window物件所構築的全域環境執行
	- statement、expression 會於全域環境下執行
	- 函式宣告、var變數宣告由於在編譯期間就已經分配記憶體給他們，且在ES6之前，會將這些當作是window物件的屬性，如下圖的x = 5會等同於window.x = 5 
```
<script>
var x = 5;
</script>
```
  如下圖的test()，可以等同於window.test()來呼叫
```
<script>
	cosole.log(window.test())
	console.log(test())
	function test() {
		console.log('hiiiii')
	}
	
</script>
```

## 若針對window增加屬性的話

```
<script>
window.testvar = 5;
console.log(testvar) // 5
console.log(window.testvar) // 5
</script>
```


## 複習
#🧠 請問在同一個DOM Document上，載入多個JS檔案，這些檔案會如何識別全域環境來執行 ->->-> `同一個DOM Document上，載入多個JS檔案相當於在DOM Document載入多個script標籤和其內容，而瀏覽器會為每一份DOM Document下建立以window物件為首的BOM tree來讓JS操作和以window物件作為全域環境來使用，所以實際上這些JS檔案的全域環境會是共享同份DOM Document上的window物件所構築的全域環境`
<!--SR:!2022-08-22,18,250-->

#🧠 declaration for var、assignment for var 在同一個DOM Document執行會是替window物件做什麼？ ->->-> `替同個window物件增加屬性來存放對應的函式物件、var變數宣告`

#🧠 若在script標籤內寫下var x = 5，請問會相當於什麼 ->->-> `替window物件增加x屬性`
<!--SR:!2022-08-06,10,250-->

#🧠 若在script標籤內寫下let x = 5，請問會替window物件增加屬性嗎->->-> `並不會`
<!--SR:!2022-08-23,19,250-->

#🧠 哪些語法在script標籤內存在，會替window物件增加屬性？ ->->-> `函式宣告、var變數宣告`
<!--SR:!2022-08-06,10,250-->

#🧠  若在script標籤內寫下函式宣告function test()，請問相當於什麼->->-> `替window物件增加對應函式物件。`
<!--SR:!2022-08-06,10,250-->

#🧠 在html檔案內，針對script而寫下window.testvar = 5，會增加全域變數嗎？ ->->-> `會，等同於替全域環境增加一個全域變數testvar，並且等於5`
<!--SR:!2022-08-20,16,250-->

---
Status: #🌱 
Tags: 
[[JavaScript]]
Links:
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]
References: