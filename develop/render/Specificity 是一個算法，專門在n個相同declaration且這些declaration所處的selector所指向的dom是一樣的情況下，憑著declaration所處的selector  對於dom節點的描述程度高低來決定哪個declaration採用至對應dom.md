

## 描述

[[@mdnSpecificityCSSCascading]]
> Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. 
> 
> The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.


重點：
- Specificity 是一個算法，專門在n個相同declaration且這些declaration所處的selector所指向的dom是一樣的情況下，憑著declaration所處的selector  對於dom節點的描述程度高低來決定哪個declaration採用至對應dom節點
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
	- id-class-type
	- id 表示目前declaration 所在的 selector 有使用 id 來描述對應元件的具體程度，會用數字表示：
		- 對應元件在同一個由多個selector構成的selector上相符N個id selector的描述，就+N-0-0。
		- 數字越高就表示在用特定id形式描述該元件上的具體程度就越高
	- class 表示目前declaration 所在的 selector 有使用 class 來描述對應元件的具體程度，會用數字表示：
		- 對應元件在同一個由多個selector構成的selector上相符N個class selector的描述，就0-+N-0
		- 數字越高就表示在以用特定class形式描述該元件的具體程度就越高
	- type 表示目前declaration 所在的 selector 有使用 type 來描述對應元件的具體程度，會用數字表示：
		- 對應元件在同一個由多個selector構成的selector上相符N個type selector的描述，就0-0-+N
		- 數字越高就表示在以用特定type形式描述該元件的具體程度就越高
	- 在這裡可以將!important為10000、inline style為1000、id部分為100分，class當作10分，type當作1分來分別表示以下意義：
		- 計算總分：將轉換分數通通加起來
		- 描述具體程度：id會是最高，class是次高，type是最後
- 特例：
	- 在多個屬性名稱上起衝突的declaration / 多個屬性名稱上是一樣的declaration，declaration都拿到一樣的權重，就挑選最後出現的declaration為主
	- 位處於universal selector 的 declaration 所獲得權重為 0-0-0 (id-class-type)，或者以數字來表説就是0分
	- 特定元件上的inline style 會算是selector，style裡頭的declaration所獲得的權重相當於1-0-0-0 (x-id-class-type) ，換成數字系統的話，會是算1000分
	- 被綁定!important的declaration 所獲得的權重為相當於是最高，為1-0-0-0-0 (xx-x-id-class-type)，換成數字系統的話，會是算10000分
- 權重是？則是將人類認為的具體認知轉換成數值



### 案例
```
.type1 #id3 {color: green; font-size: 20px;} 
div p #id3 {color: blue; background-color: grey;} 
```

> 假設這2行代碼都能夠選中同一個ID為「id3」的元素，且都是出自同一來源的樣式表。可以看到，二者使用的優先級最高的選擇器都是ID選擇器，起衝突的樣式設定是字型顏色。一個給此元素設定字型顏色為綠色，另一個給此元素設定字型顏色為藍色。按照評分規則，因為前一種代碼使用了1個類選擇器和1個id選擇器，所以得分為10+100=110分；後一種代碼使用了2個標籤選擇器和1個id選擇器，所以得分為1+1+100=102分。因為110分>102分，所以前一種規則勝出，目標元素的最終文字顏色應該是綠色。



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
<!--SR:!2025-03-20,567,250-->

#🧠 specific 命名緣由為何？ ->->-> `是指清晰和正確`
<!--SR:!2024-01-02,296,250-->

#🧠 CSS specificity 是什麼？->->-> `Specificity 是一個算法，專門在n個相同declaration且這些declaration所處的selector所指向的dom是一樣的情況下，憑著declaration所處的selector 對於dom節點的描述程度高低來決定哪個declaration採用至對應dom`
<!--SR:!2023-10-31,71,228-->


#🧠 CSS Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，請問declaration包含了哪些情況？(名稱重複？！) ->->-> `這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突`
<!--SR:!2023-11-07,78,210-->

#🧠 CSS Specificity 是一個算法，專門在n個相同declaration且這些declaration所處的selector所指向的dom是一樣的情況下，憑著declaration所處的selector 對於dom節點的描述程度高低來決定哪個declaration採用至對應dom，那麼主要會如何選擇？(面對於重複和沒重複的情況下) ->->-> `主要會用權重來衡量每個declaration、 多個屬性名稱上起衝突的declaration / 多個屬性名稱上是一樣的declaration，就選擇權重最高的declaration，並納入至它所對應元件會有的樣式屬性、屬性名稱沒起衝突的declaration ，就直接納入至它所對應元件會有的樣式屬性`
<!--SR:!2023-12-27,293,250-->

#🧠 在CSS Specificity中，每一個declaration權重形式是何種形式 ->->-> `基本上會使用三種欄位值，分別為id、class、type，形式為id-class-type`
<!--SR:!2024-04-05,358,250-->


#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼id代表著什麼？ ->->-> `表示目前declaration 所在的 selector 有使用 id 來描述對應元件的具體程度，會用數字表示`
<!--SR:!2023-12-17,173,230-->

#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼id代表目前declaration 所在的 selector 有使用 id 來描述對應元件的具體程度，會用數字表示，那麼具體如何用數字表示？ ->->-> `對應元件在同一個由多個selector構成的selector上相符N個id selector的描述，就+N-0-0。、 數字越高就表示在用特定id形式描述該元件上的具體程度就越高`
<!--SR:!2024-10-19,474,250-->

#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼class代表著什麼？ ->->-> ` class 表示目前declaration 所在的 selector 有使用 class 來描述對應元件的具體程度，會用數字表示`
<!--SR:!2024-06-07,340,230-->


#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼class代表著目前declaration 所在的 selector 有使用 class 來描述對應元件的具體程度，會用數字表示，那麼具體如何用數字表示？->->-> `對應元件在同一個由多個selector構成的selector上相符N個class selector的描述，就0-+N-0、數字越高就表示在以用特定class形式描述該元件的具體程度就越高`
<!--SR:!2024-06-08,394,250-->

#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼type代表著什麼？->->-> `type 表示目前declaration 所在的 selector 有使用 type 來描述對應元件的具體程度，會用數字表示`
<!--SR:!2024-02-05,319,250-->

#🧠 在CSS Specificity中，每一個declaration權重形式是三種欄位值，分別為id、class、type，形式為id-class-type，那麼type表示目前declaration 所在的 selector 有使用 type 來描述對應元件的具體程度，會用數字表示，具體如何用數字表示？ ->->-> `對應元件在同一個由多個selector構成的selector上相符N個type selector的描述，就0-0-+N、數字越高就表示在以用特定type形式描述該元件的具體程度就越高`
<!--SR:!2024-01-13,234,230-->


#🧠 CSS specificitiy上的id-class-type，若要統一轉換成數字來看的話，可以是如何計算？？ 如何比較->->-> `id-class-type，1個id為100分、1個class為10分、1個type為1分，並將計算總分，將轉換分數通通加起來。比較的話，就挑出最大者的declaration來使用`
<!--SR:!2024-01-20,307,250-->

#🧠 在CSS Specificity中的id-class-type 計算中，那如何將特例下的!important、inline style計算權重？那id、class、type的分數是如何？->->-> `每個!important 為10000分、每個inline style為1000分。每一個id、每一個class、每一個type分數分別為100、10、1分`
<!--SR:!2024-02-26,332,250-->

#🧠 在CSS specificity中，多個屬性名稱上起衝突的declaration / 多個屬性名稱上是一樣的declaration，declaration都拿到一樣的權重，會如何決定最後的declaration? ->->-> `就挑選最後出現的declaration為主`
<!--SR:!2025-02-26,551,250-->

#🧠 在CSS specificity中，位處於universal selector 的 declaration 所獲得權重為何？ 換算上分數的話，會是多少分？->->-> `0-0-0，0分`
<!--SR:!2024-10-25,480,250-->

#🧠 在CSS specificity中，declaration在哪種情況下獲得權重是最高的？形式會是如何？->->-> `用!important來綁定的declaration，形式會是 background-color: red !important;`
<!--SR:!2024-01-04,298,250-->

#🧠 在CSS specificity中，declaration在哪種情況下獲得權重是次高的？形式會是如何？ ->->-> `用inline style是來綁定declaration block，<div style="font-size:24px;color:red;"> </div>`
<!--SR:!2023-10-29,65,210-->

#🧠 在CSS specificity中，被綁定!important的declaration 所獲得的權重為相當於是最高，那麼可以轉換成什麼形式和數字 ->->-> `1-0-0-0-0，分數為10000`
<!--SR:!2024-02-07,318,250-->

#🧠 在CSS specificity中，被綁定inline 的declaration 所獲得的權重為相當於是次高，那麼可以轉換成什麼形式和數字 ->->-> `0-1-0-0-0，分數為1000`
<!--SR:!2024-10-20,474,250-->


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