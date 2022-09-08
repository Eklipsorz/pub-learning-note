## 描述

### 文獻
[[@mdnPositionCSSCascading]]
> The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block.

邊界

重點：
- absolute-positioning 元素本身會依據最近的positioned parent 元素所擁有邊界為位移的範疇：
	- positioned parent 元素：包覆著absolute-positioning 元素的元素
	- 若沒有position parent元素，就以viewport的邊界來位移
- absolute-positioning 元素本身脫離


### position 屬性值


  


5. 若position 設定為absolute時，其容器大小會跟著內容而變化，而定位方式會從static改變，且以離該元素最近的定位父元素(ancestor element，其position被設定static以外的值)所擁有定為參考點為基準點(圖中橘點)來定位，而定位方式是以該元素邊界和父元素邊界在父元素內部之間的距離作為基準點來調整top、bottom、left、right，類似於position: fixed的定位方式，只是差別在於還會挑有定位過的父元素，若一直都找不到合適的父元素(ancestor element)的話，才會以Viewport邊界和其元素邊界之差來呈現。

  

(原文： is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport.) However, if an absolute positioned element has no positioned ancestor, it uses the document body, and move along with page scrolling.)

  

其top、bottom、left、right的移動方式會如同設定fixed那樣去決定元素的定位。



## 複習


---
Status: #🌱 
Tags:
[[CSS]] - [[HTML]]
Links:
References:
[[@mdnPositionCSSCascading]]