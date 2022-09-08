## 描述

### 文獻
[[@mdnPositionCSSCascading]]
> The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block.

邊界

重點：
- absolute-positioning 元素本身會依據最近的positioned parent 元素所擁有邊界(margin)為位移的範疇：
	- positioned parent 元素：包覆著absolute-positioning 元素的元素
	- 若沒有position parent元素，就以viewport的邊界來位移
- absolute-positioning 元素本身脫離normal flow/flow layout的控制，換言之，normal flow/flow layout不會考慮absolute-positioning來處理，比如會為了呈現它而多留空白。
- absolute-positioning 元素在沒特別設定width、height的情況下，會為了滿足top、bottom、left、right而調整其元素的高寬。

### position 屬性值



  若position 設定為absolute時，其容器大小會跟著內容而變化，而定位方式會從static改變，且直接在positioning parent元件邊界(margin)定位，定位方式是以元素和viewport這兩者間的邊界(margin)距離作為基準點，整體來說會像是：


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643938/blog/htmlPosition/absolute-position/absolute-positioning-view_rtw4jn.png)




其top、bottom、left、right的移動方式會如同設定fixed那樣去決定元素的定位。

### value1 為正值

當absolute-positioning 元素找到適合的positioned parent 元素A，就會以它的邊界(margin)來位移

a. 當對absolute-positioning 元素的top為value1，其元素的上邊界和parent元素A的上邊界
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-top-case_y0kwrz.png)




![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-bottom-case_evsu4h.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-right-case_zxfga3.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-right-case_zxfga3.png)



## 複習


---
Status: #🌱 
Tags:
[[CSS]] - [[HTML]]
Links:
References:
[[@mdnPositionCSSCascading]]