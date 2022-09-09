## 描述

### 文獻
[[@mdnPositionCSSCascading]]
> The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block.

邊界

重點：
- absolute-positioning 元素本身會依據最近的positioned parent 元素所擁有邊界(margin)為位移的範疇：
	- positioned parent 元素：包覆著absolute-positioning 元素的元素
	- 若沒有position parent元素，就以viewport的邊界來位移
- absolute-positioning 元素本身脫離normal flow/flow layout的控制，換言之，normal flow/flow layout不會考慮absolute-positioning來處理，比如不會為了呈現它而多留空白。
- absolute-positioning 元素在沒特別設定width、height的情況下，會為了滿足top、bottom、left、right而調整其元素的高寬。

### position 屬性值



  若position 設定為absolute時，其容器大小會跟著內容而變化，而定位方式會從static改變，且直接在positioning parent元件邊界(margin)定位，定位方式是以元素和viewport這兩者間的邊界(margin)距離作為基準點，整體來說會像是：


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643938/blog/htmlPosition/absolute-position/absolute-positioning-view_rtw4jn.png)




其top、bottom、left、right的移動方式會如同設定fixed那樣去決定元素的定位。

### value1 為正值

當absolute-positioning 元素找到適合的positioned parent 元素A，就會以它的邊界(margin)來位移

a. 當對absolute-positioning 元素的top為value1，其元素的上邊界和parent元素A的上邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-top-case_y0kwrz.png)


b. 當對absolute-positioning 元素的bottom為value1，其元素的下邊界和parent元素A的下邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-bottom-case_evsu4h.png)

當對absolute-positioning 元素的right為value1，其元素的右邊界和parent元素A的右邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-right-case_zxfga3.png)

當對absolute-positioning 元素的left為value1，其元素的左邊界和parent元素A的左邊界之間會保持著value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-left-case_orsgj2.png)

### value1 為負值


當對absolute-positioning 元素的left為value1，其元素的左邊界和parent元素A的左邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646094/blog/htmlPosition/absolute-position/absolute-positioning-left-negative-case_hxrfpd.png)


當對absolute-positioning 元素的right為value1，其元素的右邊界和parent元素A的右邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646095/blog/htmlPosition/absolute-position/absolute-positioning-right-negative-case_pgypxh.png)


當對absolute-positioning 元素的bottom為value1，其元素的下邊界和parent元素A的下邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646095/blog/htmlPosition/absolute-position/absolute-positioning-bottom-negative-case_cez5ab.png)



當對absolute-positioning 元素的top為value1，其元素的上邊界和parent元素A的上邊界之間會保持著value1的距離
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646096/blog/htmlPosition/absolute-position/absolute-positioning-top-negative-case_jbsam2.png)


## 複習

#🧠 absolute-positioning 元素會以什麼為主來位移？->->-> `最近的positioned parent 元素所擁有邊界(margin)為位移的範疇`

#🧠 absolute-positioning 元素的位移方式為何？ ->->-> ``

#🧠  absolute-positioning 元素若找不到最近的positioned parent 元素，會找誰替代？ ->->-> `就以viewport的邊界來位移`
<!--SR:!2022-09-12,3,250-->


#🧠 absolute-positioning 元素和normal flow/flow layout之間的關係為何？ ->->-> `absolute-positioning 元素本身脫離normal flow/flow layout的控制，換言之，normal flow/flow layout不會考慮absolute-positioning來處理`


#🧠 absolute-positioning 元素本身脫離normal flow/flow layout的控制，換言之，normal flow/flow layout不會考慮absolute-positioning來處理，具體不做哪些？ ->->-> `不會為了呈現它而多留空白`
<!--SR:!2022-09-12,3,250-->

#🧠 absolute-positioning 元素大小和top、bottom、left、right之間的關係是什麼？->->-> `absolute-positioning 元素在沒特別設定width、height的情況下，會為了滿足top、bottom、left、right而調整其元素的高寬`

#🧠 當對absolute-positioning 元素的top為value1，會是代表著什麼？->->-> `其元素的上邊界和parent元素A的上邊界之間會保持著value1的距離`

#🧠 當對absolute-positioning 元素的right為value1，會是代表著什麼？->->-> `其元素的右邊界和parent元素A的右邊界之間會保持著value1的距離`
<!--SR:!2022-09-12,3,250-->

#🧠 當對absolute-positioning 元素的left為value1，會是代表著什麼？ ->->-> `其元素的左邊界和parent元素A的左邊界之間會保持著value1的距離`

#🧠 當對absolute-positioning 元素的bottom為value1，會是代表著什麼？->->-> `其元素的下邊界和parent元素A的下邊界之間會保持著value1的距離`

#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為正值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-top-case_y0kwrz.png): ->->-> `設定top為value1`

#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為正值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-bottom-case_evsu4h.png) ->->-> `設定bottom為value1`
<!--SR:!2022-09-12,3,250-->

#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為正值  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-right-case_zxfga3.png)->->-> `設定right為value1`

#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為正值 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662643905/blog/htmlPosition/absolute-position/absolute-positioning-left-case_orsgj2.png)  ->->-> `設定left為value1`


#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為負值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646096/blog/htmlPosition/absolute-position/absolute-positioning-top-negative-case_jbsam2.png) ->->-> `設定top為負的value1`
<!--SR:!2022-09-12,3,250-->

#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為負值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646095/blog/htmlPosition/absolute-position/absolute-positioning-bottom-negative-case_cez5ab.png) ->->-> `設定bottom為負的value1`


#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為負值 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646095/blog/htmlPosition/absolute-position/absolute-positioning-right-negative-case_pgypxh.png)->->-> `設定right為負的value1`
<!--SR:!2022-09-12,3,250-->



#🧠 當對absolute-positioning 元素調整top、left、right、bottom屬性，怎麼調才能呈現如下，其中屬性值為負值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662646094/blog/htmlPosition/absolute-position/absolute-positioning-left-negative-case_hxrfpd.png)->->-> `設定left為負的value1`
<!--SR:!2022-09-12,3,250-->


---
Status: #🌱 
Tags:
[[CSS]] - [[HTML]]
Links:
[[當元素的position屬性被調整成非static的屬性值，就能依據著top、left、right、bottom、z-index來調整其元素的位置]]
References:
[[@mdnPositionCSSCascading]]