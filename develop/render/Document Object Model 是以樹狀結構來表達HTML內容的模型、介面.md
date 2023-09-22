## 描述

[[@mdnWenJianWuJianMoXingDOMWeb]] 所描述：

> **文件物件模型（_Document Object Model, DOM_）**是 HTML、XML 和 SVG 文件的程式介面。它提供了一個文件（樹）的結構化表示法，並定義讓程式可以存取並改變文件架構、風格和內容的方法。DOM 提供了文件以擁有屬性與函式的節點與物件組成的結構化表示。節點也可以附加事件處理程序，一旦觸發事件就會執行處理程序。 本質上，它將網頁與腳本或程式語言連結在一起。

> 雖然常常使用 JavaScript 來存取 DOM，但它本身並不是 JavaScript 語言的一部分，而且它也可以被其他語言存取（雖然不太常見就是了）。

重點：
- Document Object Model 是以樹狀結構來表達HTML內容的模型、介面
- 其模型的作用是為了
	- 讓其他程式語言能夠透過此介面、模型來操作網頁內容，如標籤
- 當瀏覽器向伺服器索取指定網頁時，伺服器將會以封包形式傳遞網頁至瀏覽器
	- 瀏覽器會邊接收邊試著組建DOM Tree

### DOM結構

DOM是種：
1. 樹狀結構的模型，其根節點是目前網站的檔案本身-document，
2. 它的子節點會是html標籤，而html標籤下的子節點就是人人熟知的head節點和body節點，再往下細分的話，也就是分別為head內含的meta資料(註1)和body內含的實際網頁呈現資料。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630065451/blog/dom/domHierarchy_tpuaxj.png)

  
  
### DOM Tree 產生
當瀏覽器已經得知對應伺服器IP是什麼，那麼使用者(瀏覽器)會再重新對該IP來要求伺服器回傳網頁的對應檔(包含了HTML檔案、CSS檔案、JavaScript檔案)給使用者的瀏覽器，而回傳檔案的形式並不會一口氣以一個完整檔案傳過去，而是以固定大小的封包(Packet)形式將原檔案切分成好幾等分傳給使用者的瀏覽器來處理。

當瀏覽器收到HTML檔案被切分出來的封包時，瀏覽器不會直接等待完整檔案被拼湊出來，而是邊收邊將收到的內容按照DOM形式來建立一個DOM節點，每一個節點都各代表一個獨立的內容或者對應標籤，當一個節點A對應原HTML檔案的標籤或者內容是在另一個節點B對應的標籤內部的話，那麼這個節點A會根據內部的深度來決定是否為節點B的子節點(Child Node)？還是為節點B的後代節點(Descendant Node)，比如說節點A對應的標籤是elementA，而節點B的標籤是elementB，若elementA還被其他元素包含著，那麼節點A就會是節點B的後代節點

```
<elementB>
	<otherElement>
		<elementA></elementA>
	</otherElement>
</elementB>
```

但若elementA沒被其他元素包含著，那麼節點A就會是節點B的子節點

```
<elementB>
	<elementA></elementA>
</elementB>
```

最後由這些節點的生成以及如何連接來構成一個樹狀結構，該樹狀結構被稱之為DOM Tree，在這個樹狀結構中會有代表HTML標籤(元件)的元素節點、代表其元件屬性的屬性節點、代表一般文字內容的文字節點以及代表註解內容的註解節點等。
  
拿下面的HTML程式碼來當例子的話：

```
<html>
	<head>
		<link rel="stylesheet" href="style.css">
	</head>
	<body>
		<h1>This is an example</h1>
		<p>Critical Rendering Path</p>
		<label>Hello World</label>

	</body>
</html>
```

在解析的過程中，會被轉化為以下樹狀結構，首先html標籤會先被瀏覽器擷取來建立一個獨立的DOM節點，接著再讀取到head標籤時，由於它是位於html標籤內部且沒其他標籤包含著，所以它會被設定成html標籤對應節點的子節點並且被html對應節點連接著，而link對應節點會因為這樣被設定成head標籤對應節點的子節點，而後body、h1、p、label也皆因為這樣而與其他節點進行連接，最後形成以下結果：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629973153/blog/RenderingPath/domTreeExample_ep0cvp.png)
  

## 註解

1. meta資料指的是定義資料的資料，如同字面上的意思，在網頁裡是負責設定以及定義一些呈現規則、要載入哪些資料的文字內容。
## 複習


#🧠 Document Object Model 是什麼？ ->->-> `Document Object Model 是以樹狀結構來表達HTML內容的模型、介面`
<!--SR:!2024-12-05,524,250-->

#🧠 Document Object Model 用途是什麼？ ->->-> `讓其他程式語言能夠透過此介面、模型來操作網頁內容，如標籤`
<!--SR:!2024-07-27,448,250-->


#🧠 Document Object Model 何時產生？ ->->-> `當瀏覽器向伺服器索取指定網頁時，伺服器將會以封包形式傳遞網頁至瀏覽器，瀏覽器會邊接收邊試著組建DOM Tree`
<!--SR:!2024-09-08,471,250-->


#🧠 DOM是種樹狀結構的模型，能簡單描述它常見的結構嗎？以一份html檔案為主，其檔案擁有html標籤、head標籤、body標籤 ->->-> `其根節點是目前網站的檔案本身-document，它的子節點會是html標籤，而html標籤下的子節點就是人人熟知的head節點和body節點，再往下細分的話，也就是分別為head內含的meta資料(註1)和body內含的實際網頁呈現資料。![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630065451/blog/dom/domHierarchy_tpuaxj.png)`
<!--SR:!2023-12-08,77,210-->

#🧠 DOM模型中，除了document這節點，其餘節點會是網頁的什麼？(畫面？) ->->-> `其document對應文件的各個標籤`
<!--SR:!2024-12-11,527,250-->


#🧠 請問伺服器如何傳遞網頁？(網路封包) ->->-> `會以一個封包能乘載的大小來將整份網頁分割成好幾個部分來傳遞`
<!--SR:!2024-02-21,350,250-->

#🧠 請問瀏覽器接收到HTML檔案被切分出來的封包時，會做什麼？ ->->-> `當瀏覽器收到HTML檔案被切分出來的封包時，瀏覽器不會直接等待完整檔案被拼湊出來，而是邊收邊將收到的內容按照DOM形式來建立一個DOM節點`
<!--SR:!2025-04-06,591,250-->


#🧠 若伺服器傳遞一份HTML至瀏覽器，瀏覽器會如何解析成DOM？其結果會是？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658586368/blog/RenderingPath/dom-example-code_pxoigr.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629973153/blog/RenderingPath/domTreeExample_ep0cvp.png)`
<!--SR:!2024-04-24,388,250-->


---
Status: #🌱 
Tags
[[JavaScript]] - [[HTML]]
Links:
References:
[[@mdnWenJianWuJianMoXingDOMWeb]]