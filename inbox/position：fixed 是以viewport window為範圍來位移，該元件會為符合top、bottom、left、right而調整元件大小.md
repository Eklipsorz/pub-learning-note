## 描述


### 文獻 

[[@w3cCSSAbsoluteFixed]]
> Fixed positioning is really just **a specialized form of absolute positioning**; elements with fixed positioning are fixed relative to the viewport/browser window rather than the containing element; even if the page is scrolled, they stay in exactly the same position inside the browser window

> The element is removed from the normal document flow, and no space is created for the element in the page layout.

重點：
- fixed positioning 是以viewport window 邊界為範圍來位移，而非以特定容器，所以即使頁面有進行滾動，其位移方式仍會以整個window為主，而非以特定頁面內容。
- fixed positioning 的元件會為了符合top、bottom、left、right而調整其元件大小。
- fixed positioning 的元件會脫離normal flow/flow layout所控制，換言之，normal flow/flow layout會不考量fixed positionging來處理，也不會為了呈現它而特意留些空間。
### position：fixed
若position 設定為fixed時，其容器大小會跟著內容而變化，而定位方式會從static改變，且直接在viewport內部定位，定位方式是以元素和viewport這兩者間的邊界距離作為基準點，viewport會由window物件來承擔，整體來說會像是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positioning-origin_afwu1z.png)

  
### value1 為正值。

在這情況下設定top、bottom、left、right時，會以最近的window邊線當作基準：

  
當value1為正值，會盡量使元素放置在viewport內部

- top設定為value1，元素的上邊界(border-top)會跟viewport的上邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-top-case_vzczxd.png)

  
- bottom設定value1，元素的下邊界(border-bottom)會跟viewport的下邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-bottom-case_coyyts.png)

  

- left設定value1，元素的左邊界(border-left)會跟viewport的左邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-left-case_ec2f10.png)

  

- right設定value1，元素的右邊界(border-right)會跟viewport的右邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-right-case_xa3f8t.png)

  
### value 1 為負值

當value1為負值，其相關邊界會從viewport外部向內部展開，比如說當top的value1為負時，元素上邊界會與viewport上邊界在viewport在外部保持value1的距離。


- left設定value1，元素的左邊界(border-right)會跟viewport的左邊界之間的距離會是value1(不考慮正負)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662575597/blog/htmlPosition/fixed-position/fixed-position-left-negative-case_ykvmvj.png)

- right 設定value1，元素的右邊界(border-right)會跟viewport的右邊界之間的距離會是value1(不考慮正負)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662575597/blog/htmlPosition/fixed-position/fixed-position-right-negative-case_kd9g5w.png)

- top 設定value1，元素的上邊界(border-right)會跟viewport的上邊界之間的距離會是value1(不考慮正負)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662575597/blog/htmlPosition/fixed-position/fixed-position-top-negative-case_a3xrje.png)

- bottom 設定value1，元素的下邊界(border-right)會跟viewport的下邊界之間的距離會是value1(不考慮正負)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662575597/blog/htmlPosition/fixed-position/fixed-position-bottom-negative-case_n1vtz9.png)





#### top、bottom、left、right共存案例：
另外當同時使用top、bottom、left、right時，會自動調整元素高寬來滿足其設定值，比如說若設定類似以下語法時，

```
left: value1
right: value2
```


其結果會是：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576351/blog/htmlPosition/fixed-position/leftrightFixedExample_qi6xtb.png)


### port 命名緣由

> A port on a computer is a place where you can attach another piece of equipment

重點：
- 在電腦科學中，port相當於一個存取介面，可允許裝置/資訊安裝至介面，以此讓使用介面的使用者能夠透過介面來存取裝置/資訊

### viewport 是什麼？
[[@mdnViewportMDNWeb]]
> A viewport represents a polygonal (normally rectangular) area in computer graphics that is currently being viewed. In web browser terms, it refers to the part of the document you're viewing which is currently visible in its window (or the screen, if the document is being viewed in full screen mode). Content outside the viewport is not visible onscreen until scrolled into view.

[[@mdnViewportShuYuBiaoMDN]]
> 一個 viewport（視圖、視區）在電腦圖像中表示一個正在被觀看的多邊型區域（通常是方形）。在瀏覽器的術語中，它指涉的是在視窗中（如果在全螢幕模式底下，那也可以是在螢幕中），正在瀏覽的文件中可被看見的一部分。在 viewport 外的內容在螢幕上是看不到的，直到內容被滾動到畫面中。

view：
>what you can see from a particular place, or the ability to see from a particular place


viewport 就是瀏覽器的最大可視範圍：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662570959/blog/htmlPosition/fixed-position/viewport_cubb2s.png)

重點：
- viewport 命名緣由為view為特定位置所能看到的畫面，port是存取介面，合併起來專門接收並存取畫面渲染資訊的存取介面
- 在電腦科學中，就是指window，會是以一個固定大小的可視區塊來呈現特定渲染內容，其中該區塊會以邊線來表示區塊的範疇
- 若進一步套用在瀏覽器的話，瀏覽器中用呈現畫面的部分就是viewport

## 複習

#🧠 port 命名緣由? ->->-> `在電腦科學中，port相當於一個存取介面，可允許裝置/資訊安裝至介面，以此讓使用介面的使用者能夠透過介面來存取裝置/資訊`

#🧠 viewport 命名緣由？ ->->-> `view為特定位置所能看到的畫面，port是存取介面，合併起來專門接收並存取畫面渲染資訊的存取介面`

#🧠 viewport 在電腦科學會是指什麼？->->-> `就是指window，會是以一個固定大小的可視區塊來呈現特定渲染內容，其中該區塊會以邊線來表示區塊的範疇`

#🧠 電腦科學 的 viewport套用在瀏覽器，則會是指什麼？ ->->-> `若進一步套用在瀏覽器的話，瀏覽器中用呈現畫面的部分就是viewport`

#🧠 normal flow/flow layout 會如何考量fixed positioning 的元件是如何排版？->->-> `fixed positioning 的元件會脫離normal flow/flow layout所控制，換言之，normal flow/flow layout會不考量fixed positionging來處理，也不會為了呈現它而特意留些空間`

#🧠 fixed positioning 的元件會從normal flow/flow layout移除，換言之，normal flow/flow layout會不考量fixed positionging來處理，比如不會做哪些事？ ->->-> `不會為了呈現它而特意留些空間`

#🧠 fixed positioning 會以什麼為主來位移？->->-> `fixed positioning 是以viewport window 邊界為範圍來位移`

#🧠 若瀏覽器有滾動軸，請問fixed positioning 會以什麼為主來位移 ->->-> `即使頁面有進行滾動，其位移方式仍會以整個window為主，而非以特定頁面內容`


#🧠 若瀏覽器有滾動軸，請問fixed positioning 為何還以viewport為主來位移? ->->-> `因為滾動軸滾動本身就只是特定頁面內容，而那不是viewport的一部分。`

#🧠 fixed positioning 的top、bottom、left、right的屬性值帶來的位移和 元素大小之間有何關係？->->-> `fixed positioning 的元件會為了符合top、bottom、left、right而調整其元件大小`

#🧠 當對fixed positioning的元件設定top、bottom、left、right屬性時會呈現以下結果，請問是設定了哪個屬性？其屬性值是正值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-top-case_vzczxd.png) ->->-> `是設定top:value1`

#🧠 當對fixed positioning的元件設定正值的value1給top屬性，會是代表著？ ->->-> `元素的上邊界(border-top)會跟viewport的上邊界在viewport內部保持value1的距離`

#🧠 當對fixed positioning的元件設定top、bottom、left、right屬性時會呈現以下結果，請問是設定了哪個屬性？其屬性值是正值 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-bottom-case_coyyts.png)->->-> `設定bottom屬性值為value1`

#🧠 當對fixed positioning的元件設定正值的value1給bottom屬性，會是代表著？->->-> `元素的下邊界(border-bottom)會跟viewport的下邊界在viewport內部保持value1的距離`

#🧠 當對fixed positioning的元件設定top、bottom、left、right屬性時會呈現以下結果，請問是設定了哪個屬性？其屬性值是正值![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662576226/blog/htmlPosition/fixed-position/fixed-positoning-left-case_ec2f10.png) ->->-> `是設定left屬性為value1`

#🧠 當對fixed positioning的元件設定正值的value1給left屬性，會是代表著？ ->->-> `元素的左邊界(border-left)會跟viewport的左邊界在viewport內部保持value1的距離`


#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``





---
Status: #🌱 #📓 
Tags:
[[CSS]]
Links:
[[具有position：relative 的元素A會以position：static的元素A的放置起點來作為位移的起始點，可透過top、left、right、bottom來位移]]
References:
[[@w3cCSSAbsoluteFixed]]
[[@mdnViewportMDNWeb]]
[[@mdnViewportShuYuBiaoMDN]]