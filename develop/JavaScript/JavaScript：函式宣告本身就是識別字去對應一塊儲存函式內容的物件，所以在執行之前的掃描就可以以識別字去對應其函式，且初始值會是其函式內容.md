## 描述
在JavaScript 中，函式一旦以下面形式來宣告的話，其可以被拆解成：函式關鍵字function、函式名稱bar，a, b, c... 是函式參數，而code則是函式內的執行程式碼。
```
function bar(a, b, c, ...) {
	// code
}
```

但其實系統會是會將bar 視為一個變數，而function關鍵字、參數、程式碼則是一個物件會存放的內容，只是在這裡會將物件參照指派給bar，如下面這樣
```
bar = function(a, b, c, ....) {
	// code
}
```

在這裡function 會稱作是以函式來表達對應值的function value，
```
function(a, b, c, ....) {
	// code
}
```




所以若考慮在Execution Conetext建立時期的話，當掃描到函式時，
```
function bar(a, b, c, ...) {
	// code
}
```

會因為函式本身的特殊宣告方式-函式本身當成物件指派給變數bar，而可以在相關的EnvironmentRecord設定成
```
xxxx: function(a, b, c, ....)
```

而xxxx 識別字對應的物件所獲取的初始值就會是函式本身
```
function (a, b, c, ...) {
	// code
}
```

## 複習
#🧠 在JavaScript 中，函式一旦以下面形式來宣告的話，可以拆解成哪幾個部分？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655359457/blog/javascript/function/function-declaration_a7ls5l.png)  ->->-> `函式關鍵字function、函式名稱bar，a, b, c... 是函式參數，而code則是函式內的執行程式碼。`
<!--SR:!2022-07-28,28,250-->

#🧠 在JavaScript 中，函式一旦以下面形式來宣告的話，可以等同什麼(提示變數被指派某值) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655359457/blog/javascript/function/function-declaration_a7ls5l.png) ->->-> `但其實系統會是會將bar 視為一個變數，而function關鍵字、參數、程式碼則是一個物件會存放的內容，只是在這裡會將物件參照指派給bar![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655359457/blog/javascript/function/function-assignment_aj6zul.png)`
<!--SR:!2022-07-28,28,250-->

#🧠 若考慮在Execution Conetext建立時期的話，當掃描到函式時，會如何識別函式？->->-> `會因為函式本身的特殊宣告方式-函式本身當成物件指派給變數bar，而可以在相關的EnvironmentRecord設定成 xxxx: function(a, b, c, ....)，而xxx識別字對應的物件所獲取的初始值就是函式本身`
<!--SR:!2022-07-15,18,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@simpsonYouDonKnow2022]]