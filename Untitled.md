## 描述


### 文獻 

[[@w3cCSSAbsoluteFixed]]
> Fixed positioning is really just **a specialized form of absolute positioning**; elements with fixed positioning are fixed relative to the viewport/browser window rather than the containing element; even if the page is scrolled, they stay in exactly the same position inside the browser window

重點：
- fixed positioning 是以viewport window為主的定位方式，而非以特定容器，所以即使頁面有進行滾動，其定位方式仍會以整個window為主
- 在這裡會以window的最左上角

###



4. 若position 設定為fixed時，其容器大小會跟著內容而變化，而定位方式會從static改變，且直接在viewport內部定位，定位方式是以元素和viewport這兩者間的邊界距離作為基準點，通常viewport會由body元素來承擔，整體來說會像是：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711523/blog/htmlPosition/originFixed_gy0g62.png)

  

在這情況下設定top、bottom、left、right時，會以最近的邊線當作基準：

  

當value1為正值，會盡量使元素放置在viewport內部

- top設定為value1，元素的上邊界(border-top)會跟viewport的上邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/topFixed_yavtfv.png)

  

- bottom設定value1，元素的下邊界(border-bottom)會跟viewport的下邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/bottomFiexd_h9olxv.png)

  

- left設定value1，元素的左邊界(border-left)會跟viewport的左邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/leftFixed_czb3te.png)

  

- right設定value1，元素的右邊界(border-right)會跟viewport的右邊界在viewport內部保持value1的距離

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629711353/blog/htmlPosition/rightFixed_bewenm.png)

  

當value1為負值，其相關邊界會從viewport外部向內部展開，比如說當top的value1為負時，元素上邊界會與viewport上邊界在viewport在外部保持value1的距離。

  

另外當同時使用top、bottom、left、right時，會自動調整元素高寬來滿足其設定值，比如說若設定類似以下語法時，

```

left: value1

right: value2

```

  

其結果會是：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629713038/blog/htmlPosition/leftrightFixedExample_gfitur.png)


### port 命名緣由

> A port on a computer is a place where you can attach another piece of equipment

重點：
- 在電腦科學中，port相當於一個存取介面，可允許裝置/資訊安裝至介面，以此讓使用介面的使用者能夠透過介面來存取裝置/資訊

### viewport 是什麼？
[[@mdnViewportMDNWeb]]
> A viewport represents a polygonal (normally rectangular) area in computer graphics that is currently being viewed. In web browser terms, it refers to the part of the document you're viewing which is currently visible in its window (or the screen, if the document is being viewed in full screen mode). Content outside the viewport is not visible onscreen until scrolled into view.

[[@mdnViewportShuYuBiaoMDN]]
> 一個 viewport（視圖、視區）在電腦圖像中表示一個正在被觀看的多邊型區域（通常是方形）。在瀏覽器的術語中，它指涉的是在視窗中（如果在全螢幕模式底下，那也可以是在螢幕中），正在瀏覽的文件中可被看見的一部分。在 viewport 外的內容在螢幕上是看不到的，直到內容被滾動到畫面中。

viewport 就是瀏覽器的最大可視範圍：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662570959/blog/htmlPosition/fixed-position/viewport_cubb2s.png)

重點：
- viewport 命名緣由：一個專門接收渲染資訊並渲染的存取介面
- 在電腦科學中，就是指window，會是以一個固定大小的可視區塊來呈現特定渲染內容，其中該區塊會以邊線來表示區塊的範疇
- 若進一步套用在瀏覽器的話，其瀏覽器的window本身就是viewport

## 複習


---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[具有position：relative 的元素A會以position：static的元素A的放置起點來作為位移的起始點，可透過top、left、right、bottom來位移]]
References:
[[@w3cCSSAbsoluteFixed]]
[[@mdnViewportMDNWeb]]
[[@mdnViewportShuYuBiaoMDN]]