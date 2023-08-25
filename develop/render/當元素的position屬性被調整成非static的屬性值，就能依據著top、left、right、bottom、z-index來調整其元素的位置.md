## 描述


### position 屬性
[[@mdnPositionCSSCascading]]
> The position CSS property sets how an element is positioned in a document. 

> The top, right, bottom, and left properties determine the final location of positioned elements.

重點：
- position 屬性是指定元件在同一份文件中的定位方式是如何
- 能填入的值，預設是static
```
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;
```
- position 屬性具體為 **在特定定位方式中，來定義 top、bottom、left、right、z-index 屬性如何調整元素位置**

### top、bottom、left、right 屬性
[[@mdnTopCSSCascading]]
> The top CSS property participates in specifying the vertical position of a positioned element. It has no effect on non-positioned elements.

[[@mdnBottomCSSCascading]]  
> The top CSS property participates in specifying the vertical position of a positioned element. It has no effect on non-positioned elements.

[[@mdnRightCSSCascading]]
> The right CSS property participates in specifying the horizontal position of a positioned element. It has no effect on non-positioned elements.

[[@LeftCSSCascading]]
> The left CSS property participates in specifying the horizontal position of a positioned element. It has no effect on non-positioned elements.

重點：
- top、bottom主要調整positioned element的垂直位置，即為上下這兩個方向
- right、left主要調整positioned element的水平位置，即為左右這兩個方向
- top、bottom、right、left 不會調整non-positioned element的水平垂直位置
- 這些屬性值會考量每個元件的margin來位移

### z-index  屬性
[[@mdnZindexCSSCascading]]
> The z-index CSS property sets the z-order of a positioned element and its descendants or flex items. Overlapping elements with a larger z-index cover those with a smaller one.

> z-index: 該屬性定義另一種維度來控制多個元素在相同位置上的呈現順序-深度，其屬性值越大，就越先呈現，數值越小，就越後呈現，但這不表示多個元素在相同位置的呈現會因為數值大而被覆蓋掉，而是以多個屬性能夠呈現為目標來達到此屬性值的效果。

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629726946/blog/htmlPosition/zIndexFromAC_vhpa0z.png)

  

重點：
- z-index 屬性是用來調整元素在另一個維度-深度所在的位置，主要是以數值來設定
- 在多個元素呈現上重疊在一起的時候，其中z-index數值越大的元素就越先呈現；其中z-index數值越小的元素就越後呈現


#### positioned element 是什麼？
[[@mdnPositionCSSCascading]]
> A positioned element is an element whose computed position value is either relative, absolute, fixed, or sticky (In other words, it's anything except `static`.)

重點：
- 在CSS中，poitioned element  會是指該元素是可受到top、bottom、left、right、z-index這五種屬性值來調整其位置，通常會是指帶有poition：relative | absolute | fixed | sticky 的元素。
- 若position 為static的元素，就是non-positioned element


#### position：static
[[@mdnPositionCSSCascading]]
> The element is positioned according to the normal flow of the document. The top, right, bottom, left, and z-index properties have no effect. This is the default value.


重點：
- 若元件的position屬性是static，就按照文件的正常排版方式來排版呈現，不會被top、bottom、left、right、z-inde來影響

## 複習

#🧠 Flow layout vs. data flow 在前端會是什麼？ ->->-> `前者為瀏覽器對於每個元素的預設排版方式；後者為資料和UI的改變方向`
<!--SR:!2023-11-01,69,209-->

#🧠 CSS：positioned element的位移會考量到元素的border？margin? ->->-> `margin`
<!--SR:!2025-02-03,532,250-->

#🧠 CSS：若位移的話，positioned element 和margin之間的關係是什麼？比如拿什麼位移->->-> `若要位移的話，會以元素的margin為單位來位移。`
<!--SR:!2023-12-05,106,230-->

#🧠 CSS：position 屬性是什麼？ ->->-> `指定元件在同一份文件中的定位方式是如何`
<!--SR:!2023-12-11,210,230-->

#🧠 CSS：position 屬性能填入的值是什麼？ ->->-> `static、relative、absolute、fixed、sticky`
<!--SR:!2024-07-15,329,230-->

#🧠 CSS：position 屬性預設為何？ ->->-> `static`
<!--SR:!2025-02-04,533,250-->

#🧠 position 屬性是指定元件在同一份文件中的定位方式是如何，概念上positioned element 是什麼元素？ ->->-> `**在特定定位方式中，來定義 top、bottom、left、right、z-index 屬性如何調整元素位置**`
<!--SR:!2023-11-21,261,249-->


#🧠 positioned element 是什麼->->-> `在CSS中，poitioned element  會是指該元素是可受到top、bottom、left、right、z-index這五種屬性值來調整其位置`
<!--SR:!2025-02-17,548,250-->

#🧠 positioned element 是指該元素是可受到top、bottom、left、right這四種屬性值來調整其位置，具體是什麼？ ->->-> `通常會是指帶有poition：relative | absolute | fixed | sticky 的元素`
<!--SR:!2024-02-03,218,210-->

#🧠 position 為static的元素是算positioned element？還是non-positioned element?  ->->-> `non-positioned element`
<!--SR:!2025-02-28,553,250-->

#🧠 position 為static的元素 是什麼？會不會受到top、left、right、bottom、z-index這五個屬性的影響 ->->-> `意旨為遵從文件上的預設排版方式來排版，並且不會被top、left、right、bottom、z-index這五個屬性來調整其位置。`
<!--SR:!2023-12-17,216,230-->

#🧠 top、right、bottom、left、z-index能夠調整non-positioned element的位置嗎？ ->->-> `並不能`
<!--SR:!2025-01-19,519,250-->

#🧠 CSS：top、bottom這兩個屬性是什麼？ ->->-> `top、bottom主要調整positioned element的垂直位置，即為上下這兩個方向`
<!--SR:!2023-12-25,224,230-->

#🧠 CSS：right、left這兩個屬性是什麼？ ->->-> ` right、left主要調整positioned element的水平位置，即為左右這兩個方向`
<!--SR:!2025-02-15,546,250-->


#🧠 CSS：z-index屬性是什麼？ ->->-> `z-index 屬性是用來調整元素在另一個維度-深度所在的位置，主要是以數值來設定`
<!--SR:!2025-02-14,543,250-->

#🧠 CSS：z-index屬性會運用在哪個地方 ->->-> `多個元素呈現上重疊在一起的時候`
<!--SR:!2025-02-22,549,250-->

#🧠 在多個元素呈現上重疊在一起的時候，z-index大小會如何控制呈現元素在深度這維度下的位置？->->-> `z-index數值越大的元素就越先呈現；其中z-index數值越小的元素就越後呈現`
<!--SR:!2025-01-24,524,250-->


---
Status: #🌱 
Tags:
[[CSS]] - [[Rendering]]
Links:
[[@mdnPositionCSSCascading]]
References:
[[@mdnPositionCSSCascading]]
[[@mdnTopCSSCascading]]
[[@mdnBottomCSSCascading]]  
[[@mdnRightCSSCascading]]
[[@LeftCSSCascading]]
[[@mdnZindexCSSCascading]]

