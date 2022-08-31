

## 描述

[[@mdnSpecificityCSSCascading]]
> Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. 
> 
> The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.


重點：
- Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突
`<P class="highlight">這個段落將被顯示為黃底紅字粗體。</P>`

```
例子：

p{
    font-size: 110%;
    font-family: garamond, sans-serif;
}
h2{
    color: red;
    background: white;
}

.highlight{
    color: red;
    background: yellow;
    font-weight: bold;
}
```
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661802724/blog/cssTag/css-merge-example_ms662h.png)
### CSS declaration
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]

### Specificity 如何計算
[[@mdnSpecificityCSSCascading]]
> Specificity is an algorithm that calculates the weight that is applied to a given CSS declaration. The weight is determined by the number of selectors of each weight category in the selector matching the element (or pseudo-element). If there are two or more declarations providing different property values for the same element, the declaration value in the style block having the matching selector with the greatest algorithmic weight gets applied.

> The specificity algorithm is basically a three-column value of three categories or weights - ID, CLASS, and TYPE - corresponding to the three types of selectors. The value represents the count of selector components in each weight category and is written as ID - CLASS - TYPE. The three columns are created by counting the number of selector components for each selector weight category in the selectors that match the element.



重點：
-  Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突
- 主要會用權重來衡量每個declaration 
	- 多個屬性名稱上起衝突的declaration / 多個屬性名稱上是一樣的declaration，就選擇權重最高的declaration，並納入至它所對應元件會有的樣式屬性
	- 屬性名稱沒起衝突的declaration ，就直接納入至它所對應元件會有的樣式屬性
- 每一個declaration的權重是使用三種欄位值來表示，分別為如下，主要會依據著declaration所在的selector 是用什麼形式來表示
	- id : class : type
	- id 表示目前declaration 所在的 selector 有使用 id 來描述 selector 的具體程度，會用數字表示，數字越高就表示在以用特定id形式描述該元件的具體程度就越高
	- class 表示目前declaration 所在的 selector 有使用 class 來描述 selector 的具體程度，會用數字表示，數字越高就表示在以用特定class形式描述該元件的具體程度就越高
	- type 表示目前declaration 所在的 selector 有使用 type 來描述 selector 的具體程度，會用數字表示，數字越高就表示在以用特定type形式描述該元件的具體程度就越高
	- 在這裡可以將!important為10000、inline為1000、id部分為100分，class當作10分，type當作1分來分別表示以下意義：
		- 描述具體程度：id會是最高，class是次高，type是最後
- 特例：
	-  在多個屬性名稱上起衝突的declaration / 多個屬性名稱上是一樣的declaration，declaration都拿到一樣的權重，就挑選最後出現的declaration為主
	- 位處於universal selector 的 declaration 所獲得權重為 0-0-0 (id-class-type)，或者以數字來表説就是0分
	- 特定元件上的inline style 會算是selector，style裡頭的declaration所獲得的權重相當於1-0-0-0 (x-id-class-type) ，換成數字系統的話，會是算1000分
	- 被綁定!important的declaration 所獲得的權重為相當於是最高，為1-0-0-0-0 (xx-x-id-class-type)，換成數字系統的話，會是算10000分

### Specificity
specificity
> the quality of being specific 

specific
> clear and exact

重點：
- specific 是指清晰和正確
- specificity 是指清晰和正確的程度

## 複習

#🧠 specificity 命名緣由為何？ ->->-> `是指清晰和正確的程度`

#🧠 specific 命名緣由為何？ ->->-> `是指清晰和正確`

#🧠 CSS specificity 是什麼？->->-> `Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A`

#🧠 CSS Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，請問declaration包含了哪些？(名稱重複？！) ->->-> `這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``




---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]
[[每個CSS rule 上的selector 部分，主要可以用下面形式來描述所要選擇的DOM節點會是什麼：universal selector、type selector、id selector、class selector]]
[[id 是同一份DOM文件用來識別特定節點的識別字串，class是同一份DOM文件下用來將多個特定節點分成好幾類]]
[[inline style 是在HTML內容標籤形式上所夾雜的一組特定樣式組合]]
References:
[[@mdnSpecificityCSSCascading]]