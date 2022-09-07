## 描述

###  文獻                                                       
[[@mdnPositionCSSCascading]]
> The element is positioned according to the normal flow of the document, and then offset _relative to itself_ based on the values of `top`, `right`, `bottom`, and `left`. The offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were `static`.


重點：
- 當被設定position：relative，其元素的定義參考點會以position：static元素的放置起點為主
- 其top、right、bottom、left 

### position：relative


3. 若position 設定為relative時，其容器大小並不會跟著內容而變化，而定位方式會從static改變，且以static模式下的元素之定位參考點為基準點(下圖橘點)來定位，由該橘點來構成其元素能夠位移的範圍(橘框)：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png)

  

而top、bottom、left、right在這裡的表現，會以橘點為主：

  

a. value1為正值時，

- 當top被設定為value1時，元素的黑點會以橘點為中心向下移動至value1

- 當bottom被設定為value1時，元素的黑點會以橘點為中心向上移動至value1

- 當left被設定為value1時，元素的黑點會以橘點為中心向右移動至value1

- 當right被設定value1時，元素的黑點會以橘點為中心向左移動至value1

  

b. 當value1為負值時，top、bottom、left、right的移動方向會變成反方向，比如當top被設定為目前為負值的value1時，元素的黑點會以橘點為中心向上移動至value1。

  
  

c. 若兩個彼此為相反方向共存的話，只會挑選優先權比較高的方向來調整：我們以下圖的relative元素作為例子，而所有元素皆以position: static為主：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793848/blog/htmlPosition/originPos_a8a7ma.png)

  
  

- 當left和right共存的話，只會以left為優先，比如說設定以下樣式，並讓left和right共同出現，且數值皆為10px。

```

.relative { //調整名為relative元素之樣式

position: relative;

  

/* 偏移 */

right: 10px;

left: 10px;

background: #ccc;

z-index:2;

}

```

  

其最後會挑選left作為最後的呈現結果：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629792533/blog/htmlPosition/coexist_rightAndleft_n4wfjy.png)

  

而若是挑選right的話，結果會是：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793057/blog/htmlPosition/rightRelativePos_aez4yw.png)

  
  

- 當top和bottom共存的話，只會以top為優先，比如說設定以下樣式，並讓top和bottom共同出現，且數值皆為10px。

  

```

.relative { //調整名為relative元素之樣式

position: relative;

  

/* 偏移 */

top: 10px;

bottom: 10px;

background: #ccc;

z-index:2;

}

  

```

  

其最後的呈現結果為：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793297/blog/htmlPosition/coexist_topAndbottom_cd6kib.png)

  

若是挑選到bottom的話，其呈現結果為：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793297/blog/htmlPosition/bottomRelativePos_vnl36d.png)

  

- 不為相反方向的屬性可以同時在元素呈現，bottom/top任一種和left/right任一種混搭，

比如說設定以下樣式，並讓4種屬性同時出現，且數值如下所示：

  

```

.relative {

position: relative;

  

/* 偏移 */

bottom: 10px;

top: 20px;

left: 10px;

right: 300px;

background: #ccc;

z-index:2;

}

  
  

```

  

最後的呈現效果會以top: 20px和left: 10px為主：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793622/blog/htmlPosition/coexist_fourPos_auzrtm.png)


## 複習


---
Status: 
Tags:
[[當元素的position屬性被調整成非static的屬性值，就能依據著top、left、right、bottom、z-index來調整其元素的位置]]
Links:
[[@mdnPositionCSSCascading]]
References:
