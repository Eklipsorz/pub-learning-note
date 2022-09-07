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
- position 屬性是指定元件在同一份文件中的定位方式是如何，具體會是影響 top、bottom、left、right 屬性，並藉由這四種屬性來調整元素位置

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

#### positioned element 是什麼？
[[@mdnPositionCSSCascading]]
> A positioned element is an element whose computed position value is either relative, absolute, fixed, or sticky (In other words, it's anything except `static`.)

重點：
- 在CSS中，poitioned element  會是指該元素是可受到top、bottom、left、right這四種屬性值來調整其位置，通常會是指帶有poition：relative | absolute | fixed | sticky 的元素。
- 若position 為static的元素，就是non-positioned element

## 複習

#🧠 CSS：position 屬性是什麼？ ->->-> `指定元件在同一份文件中的定位方式是如何`

#🧠 CSS：position 屬性能填入的值是什麼？ ->->-> `static、relative、absolute、fixed、sticky`

#🧠 CSS：position 屬性預設為何？ ->->-> `static`

#🧠 position 屬性是指定元件在同一份文件中的定位方式是如何 ->->-> ``

---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[@mdnPositionCSSCascading]]
References:
[[@mdnPositionCSSCascading]]
[[@mdnTopCSSCascading]]
[[@mdnBottomCSSCascading]]  
[[@mdnRightCSSCascading]]
[[@LeftCSSCascading]]

  

