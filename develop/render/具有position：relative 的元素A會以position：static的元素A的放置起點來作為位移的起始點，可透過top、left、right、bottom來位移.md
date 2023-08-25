## 描述

###  文獻                                                       
[[@mdnPositionCSSCascading]]
> The element is positioned according to the normal flow of the document, and then offset _relative to itself_ based on the values of `top`, `right`, `bottom`, and `left`. The offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were `static`.


重點：
- 當被設定position：relative，其元素的位置參考點會以position：static元素的各個邊界為主
- 其top、right、bottom、left 會是指定被位移後的元素會離位移前之間有多少位移量，其方向是如何
- 其元素的高寬不會因為為了滿足top、right、bottom、left而變化
- relative positioning 的元素仍會受到normal flow/flow layout而控制，並在那情況下調整位置
### position：relative

若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png)


#### 當設定top為value1時

會讓元素A的上邊界和元素A'的上邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往下移動；數值越小的話，會使灰色部分往上移動

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-top_cluoij.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-top_cluoij.png)


#### 當設定right為value1時

會讓元素A的右邊界和元素A'的右邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往左邊移動；數值越小的話，會使灰色部分往右邊移動


![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-right_exkpls.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-right_exkpls.png)

#### 當設定bottom為value1時

會讓元素A的下邊界和元素A'的下邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往上邊移動；數值越小的話，會使灰色部分往下邊移動

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453960/blog/htmlPosition/relative-direction/relative-position-example-bottom_xgeiqe.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453960/blog/htmlPosition/relative-direction/relative-position-example-bottom_xgeiqe.png)


#### 當設定left為value1時

會讓元素A的左邊界和元素A'的左邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往右邊移動；數值越小的話，會使灰色部分往左邊移動

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-left_tg8fbk.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-left_tg8fbk.png)


### 若兩個彼此為相反方向共存的話，只會挑選優先權比較高的方向來調整：我們以下圖的relative元素作為例子，而所有元素皆以position: static為主：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629793848/blog/htmlPosition/originPos_a8a7ma.png)

  
### 位置屬性共存問題

#### left 和 right 共存問題

當left和right共存的話，只會以left為優先，比如說設定以下樣式，並讓left和right共同出現，且數值皆為10px。

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

  
  
#### top 和 bottom 共存
當top和bottom共存的話，只會以top為優先，比如說設定以下樣式，並讓top和bottom共同出現，且數值皆為10px。

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

  
##### top 和 bottom 共存：會挑選top的原因
採取normal flow所預設的排版方向，由上而下來排，上的方向擁有的優先權比較高

##### left 和 right 共存：會挑選left的原因
採取normal flow所預設的排版方向，由左而右來排，左的方向擁有的優先權比較高


####  left 和 right 共存問題 & top 和 bottom 共存
不為相反方向的屬性可以同時在元素呈現，bottom/top任一種和left/right任一種混搭，比如說設定以下樣式，並讓4種屬性同時出現，且數值如下所示：

  
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

#🧠 relative positioning 的元素和flow layout之間的關係？ ->->-> `relative positioning 的元素仍會受到normal flow/flow layout而控制，並在那情況下調整位置`
<!--SR:!2023-09-08,219,246-->

#🧠 具有position：relative的元素A會不會因為滿足top、right、bottom、left而改變元素A的高寬？ ->->-> `不會`
<!--SR:!2023-12-02,105,228-->

#🧠 具有position：relative的元素A 高寬和元素A的top、right、bottom、left這四種屬性之間的關係是如何？ (會不會改變之類的)->->-> `其元素的高寬不會因為為了滿足top、right、bottom、left而變化`
<!--SR:!2023-09-02,217,248-->

#🧠 當被設定position：relative時，其位置會以什麼點做標準來位移？->->-> `當被設定position：relative，其元素的位置參考點會以position：static元素的各個邊界為主`
<!--SR:!2023-09-05,10,249-->

#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定top為value1時，其黑點和其元素會在哪裡？為什麼![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> `會讓元素A的上邊界和元素A'的上邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往下移動；數值越小的話，會使灰色部分往上移動`
<!--SR:!2023-09-09,14,249-->



#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定left為value1時，其黑點和其元素會在哪裡？為什麼![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> `會讓元素A的左邊界和元素A'的左邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往右邊移動；數值越小的話，會使灰色部分往左邊移動`
<!--SR:!2023-08-27,6,249-->

#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定right為value1時，其黑點和其元素會在哪裡？為什麼![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> `會讓元素A的右邊界和元素A'的右邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往左邊移動；數值越小的話，會使灰色部分往右邊移動`
<!--SR:!2023-08-26,5,249-->


#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定bottom為value1時，其黑點和其元素會在哪裡？為什麼![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> `會讓元素A的右邊界和元素A'的下邊界之間保持著value1的距離，數值越大的話，會使灰色部分越往上邊移動；數值越小的話，會使灰色部分往下邊移動`
<!--SR:!2023-09-07,12,249-->

#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定top為value1時，其黑點和其元素會在哪裡？畫圖來表示![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-top_cluoij.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-top_cluoij.png)
<!--SR:!2023-08-27,6,249-->


#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定right為value1時，其黑點和其元素會在哪裡？畫圖來表示 ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png)->->-> ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-right_exkpls.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-right_exkpls.png)
<!--SR:!2023-09-06,12,249-->


#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定bottom為value1時，其黑點和其元素會在哪裡？畫圖來表示 ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png)->->-> ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453960/blog/htmlPosition/relative-direction/relative-position-example-bottom_xgeiqe.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453960/blog/htmlPosition/relative-direction/relative-position-example-bottom_xgeiqe.png)
<!--SR:!2023-09-08,13,249-->

#🧠 若position 設定為relative時，其定位參考會是以static模式下的元素A所在的各個邊界為基準點，在這裡會將同個元素A從static設定為relative，接著令其元素會是元素A'，請問若當relative positioned element設定left為value1時，其黑點和其元素會在哪裡？畫圖來表示![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-origin_qcjlfu.png) ->->-> ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-left_tg8fbk.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692453961/blog/htmlPosition/relative-direction/relative-position-example-left_tg8fbk.png)
<!--SR:!2023-08-27,6,249-->


#🧠 在position：relative的元素下都設置著left、right這兩個屬性，請問會如何決定偏移值 ->->-> `會捨棄right這屬性，改選left為主`
<!--SR:!2023-09-06,12,249-->


#🧠 在position：relative的元素下都設置著top、bottom這兩個屬性，請問會如何決定偏移值 ->->-> `會捨棄bottom這屬性，改選top為主`
<!--SR:!2023-09-06,12,249-->


#🧠  在position：relative的元素下，top 和 bottom 中會挑選top的原因->->-> `採取normal flow所預設的排版方向，由上而下來排，上的方向擁有的優先權比較高`
<!--SR:!2023-09-09,14,249-->


#🧠 在position：relative的元素下，left 和 right 中會挑選left的原因 ->->-> `採取normal flow所預設的排版方向，由左而右來排，做的方向擁有的優先權比較高`
<!--SR:!2023-09-07,12,249-->


#🧠 在position：relative的元素下都設置著top、bottom、left、right這四種屬性，請問會如何決定偏移值(提示：以屬性共存來說) ->->-> `會選top和left這兩種屬性`
<!--SR:!2023-08-27,6,249-->


#🧠 在position：relative的元素下，若都設置著top、bottom：會挑選top的原因會是甚麼?  ->->-> `採取normal flow所預設的排版方向，由上而下來排，上的方向擁有的優先權比較高`
<!--SR:!2023-08-26,5,249-->


#🧠 在position：relative的元素下，若都設置著left、right：會挑選left的原因會是甚麼?  ->->-> `採取normal flow所預設的排版方向，由左而右來排，左的方向擁有的優先權比較高
<!--SR:!2023-08-28,5,248-->
`
<!--SR:!2023-08-21,2,249-->



---
Status: 
Tags:
[[當元素的position屬性被調整成非static的屬性值，就能依據著top、left、right、bottom、z-index來調整其元素的位置]]
Links:
[[@mdnPositionCSSCascading]]
References:
