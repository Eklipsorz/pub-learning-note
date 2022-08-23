## 描述
[[@w3schoolJavaScriptWindow]] 所描述：
> ## The Browser Object Model (BOM)
> There are no official standards for the **B**rowser **O**bject **M**odel (BOM).
> 
> Since modern browsers have implemented (almost) the same methods and properties for JavaScript interactivity, it is often referred to, as methods and properties of the BOM.

> ## The Window Object
> The `window` object is supported by all browsers. It represents the browser's window.
> All global JavaScript objects, functions, and variables automatically become members of the window object.


[[@happycodingJavaScriptRuMenXiLieBOMHeDOMBiJi]] 所描述：
> BOM 的核心其實是 window 物件。而 window 物件提供的屬性主要為 document、location、navigator、screen、history 以及 frames。

> 在瀏覽器裡的 window 物件扮演著兩種角色：
> - ECMAScript 標準裡的「全域物件」 (Global Object)
> - JavaScript 用來與瀏覽器溝通的窗口

> BOM (Browser Object Model，瀏覽器物件模型)，是瀏覽器所有功能的核心，與網頁的內容無關。早期沒有規範時，各家瀏覽器廠商自行開發瀏覽器的功能，非常混亂。 直到最近幾年， W3C 把各家瀏覽器統一集合起來納入了 HTML5 的標準中。因為在DOM Level 1標準定制前，BOM已經存在了，所以也可以稱作Level 0 DOM。


重點：
- Browser Object Model 是早期在沒有DOM時代時，以樹狀結構來表示網頁內容的介面
- BOM 用途：
	- 提供程式語言能夠透過介面來控制瀏覽器和瀏覽器下的網頁
- BOM vs. DOM 差別就在於，BOM會是以Browser作為根節點來連接DOM目前擁有的樹狀結構
- BOM 根節點為Browser 或者 Window 物件，用途為：
	- 定義全域環境歸屬於誰的全域物件，換言之，以window物件作為全域環境
	- JavaScript 用來與瀏覽器本身溝通的介面
- BOM 和 DOM現況：大部分常見瀏覽器都同時支援這兩個模型

### BOM結構

除了DOM以外，還有一種是為了能與瀏覽器本身進行互動的樹狀結構的模型-Browser Object Model，在DOM的基礎下將瀏覽器本身視為一個物件來允許其他語法與它互動，在這個模型下，其根節點是瀏覽器本身(window)，其子節點有DOM根節點-document、frames、history、location、screen，其中document節點子節點會接續著DOM剩下的內容。

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630066487/blog/dom/bomHierarchy_kp1icw.png)

  

然而W3C還未對BOM進行嚴格的規範，基本上瀏覽器對於BOM的實現會有不一致的問題，不過大部分瀏覽器都支援BOM和DOM這兩套模型，當如果要調用DOM的節點時，可以不必從BOM的根節點開始調用，直接從DOM根節點就可以實現了，然而當要調用BOM的節點時，就必須直接從BOM根節點開始進行。


## 複習
#🧠 Browser Object Model 是什麼？ ->->-> `是早期在沒有DOM時代時，以樹狀結構來表示網頁內容的介面`
<!--SR:!2022-09-02,27,250-->

#🧠 Browser Object Model 和 Document Object Model 之間的差別是什麼？ ->->-> `BOM會是以Browser作為根節點來連接DOM目前擁有的樹狀結構
<!--SR:!2022-09-03,28,250-->

#🧠 BOM 的根節點為何？->->-> `Browser 或者 Window 物件`
<!--SR:!2022-10-12,50,250-->


#🧠 BOM的window節點主要做啥? (全域和介面) ->->-> `定義全域環境歸屬於誰的全域物件，換言之，以window物件作為全域環境、JavaScript 用來與瀏覽器本身溝通的介面`
<!--SR:!2022-09-17,32,230-->


#🧠 DOM 和 BOM的現況？ ->->-> `大部分瀏覽器都支援BOM和DOM這兩套模型`
<!--SR:!2022-09-02,27,250-->


#🧠 請畫圖來表示BOM和DOM之間的關係？用樹狀圖->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630066487/blog/dom/bomHierarchy_kp1icw.png)`
<!--SR:!2022-08-29,24,250-->


---
Status: #🌱 
Tags: 
[[JavaScript]]
Links:
[[Document Object Model 是以樹狀結構來表達HTML內容的模型、介面]]
References:
[[@w3schoolJavaScriptWindow]]
[[@happycodingJavaScriptRuMenXiLieBOMHeDOMBiJi]]