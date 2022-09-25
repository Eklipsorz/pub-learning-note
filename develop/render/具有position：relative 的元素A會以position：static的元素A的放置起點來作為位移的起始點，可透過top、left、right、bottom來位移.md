## 描述

###  文獻                                                       
[[@mdnPositionCSSCascading]]
> The element is positioned according to the normal flow of the document, and then offset _relative to itself_ based on the values of `top`, `right`, `bottom`, and `left`. The offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were `static`.


重點：
- 當被設定position：relative，其元素的位置參考點會以position：static元素的放置起點為主
- 其top、right、bottom、left 會是指定被位移後的元素會離位移前之間有多少位移量，其方向是如何
- 其元素的高寬不會因為為了滿足top、right、bottom、left而變化
- relative positioning 的元素仍會受到normal flow/flow layout而控制，並在那情況下調整位置
### position：relative


若position 設定為relative時，其容器大小並不會跟著內容而變化，而定位方式會從static改變，且以static模式下的元素之定位參考點為基準點(下圖橘點)來定位，由該橘點來構成其元素能夠位移的範圍(橘框)：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png)

  
而top、bottom、left、right在這裡的表現，會以橘點為主：

### value1為正值時

1. 當top被設定為value1時，為了讓被位移後的元素離橘點擁有value1 px的上方偏移量，而讓元素的黑點會以橘點為起始點向下移動value1 px
2. 當bottom被設定為value1時，為了讓被位移後的元素離橘點擁有value1 px的下方偏移量，而讓元素的黑點會以橘點為起始點向上移動value1 px
3. 當left被設定為value1時，為了讓被位移後的元素離橘點擁有value1 px的左方偏移量，而讓元素的黑點會以橘點為起始點向右移動value1 px
4. 當right被設定value1時，為了讓被位移後的元素離橘點擁有value1 px的右方偏移量，而讓元素的黑點會以橘點為起始點向左移動至value1 px 




### value1 為負值時

當value1為負值時，top、bottom、left、right的移動方向會變成反方向，比如當top被設定為目前為負值的value1時，元素的黑點會以橘點為中心向上移動至value1。


### 總結：value1 正值 和 value2 負值

如果是調整top屬性的話，其屬性值value1若是正的話，就會將元素往下偏移；其屬性值若是負的話，就會將元素往上偏移。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-top-offset_qybhfg.png)

如果是調整bottom屬性的話，其屬性值value1若是正的話，就會將元素往上偏移；其屬性值若是負的話，就會將元素往下偏移。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-bottom-offset_x0jc6r.png)


如果是調整right屬性的話，其屬性值value1若是正的話，就會將元素往左偏移；其屬性值若是負的話，就會將元素往右偏移。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-right-offset_au8dxj.png)

如果是調整left屬性的話，其屬性值value1若是正的話，就會將元素往右偏移；其屬性值若是負的話，就會將元素往左偏移。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-left-offset_k59p4g.png)



c. 若兩個彼此為相反方向共存的話，只會挑選優先權比較高的方向來調整：我們以下圖的relative元素作為例子，而所有元素皆以position: static為主：

  

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
採取normal flow所預設的排版方向，由上而下來排

##### left 和 right 共存：會挑選left的原因
採取normal flow所預設的排版方向，由左而右來排


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
<!--SR:!2022-09-29,13,246-->

#🧠 具有position：relative的元素A會不會因為滿足top、right、bottom、left而改變元素A的高寬？ ->->-> `不會`
<!--SR:!2022-09-27,12,248-->

#🧠 具有position：relative的元素A 高寬和元素A的top、right、bottom、left這四種屬性之間的關係是如何？ (會不會改變之類的)->->-> `其元素的高寬不會因為為了滿足top、right、bottom、left而變化`
<!--SR:!2022-09-28,13,248-->

#🧠 當被設定position：relative時，其位置會以什麼點做標準來位移？->->-> `其元素的位置參考點會以position：static元素的放置起點為主`
<!--SR:!2022-09-26,12,248-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定top為正值的value1，其黑點和其元素會在哪裡？為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `為了讓被位移後的元素離橘點擁有value1 px的上方偏移量，而讓元素的黑點會以橘點為起始點向下移動value1 px`
<!--SR:!2022-10-03,16,228-->


#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定bottom被設定為正值的value1，其黑點和其元素會在哪裡？為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `為了讓被位移後的元素離橘點擁有value1 px的下方偏移量，而讓元素的黑點會以橘點為起始點向上移動value1 px`
<!--SR:!2022-10-19,28,250-->


#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定left被設定為正值的value1，其黑點和其元素會在哪裡？為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `為了讓被位移後的元素離橘點擁有value1 px的左方偏移量，而讓元素的黑點會以橘點為起始點向右移動value1 px`
<!--SR:!2022-10-01,15,248-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定right被設定為正值的value1，其黑點和其元素會在哪裡？為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> ->->-> `為了讓被位移後的元素離橘點擁有value1 px的右方偏移量，而讓元素的黑點會以橘點為起始點向左移動至value1 px `
<!--SR:!2022-10-02,15,228-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定top為負值的value1，其黑點和其元素會在哪裡？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `會往上位移-value1`
<!--SR:!2022-10-24,29,247-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定bottom為負值的value1，其黑點和其元素會在哪裡？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `會往下位移-value1`
<!--SR:!2022-10-03,17,248-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定right為負值的value1，其黑點和其元素會在哪裡？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `會往右位移-value1`
<!--SR:!2022-10-19,28,250-->


#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問若只設定left為負值的value1，其黑點和其元素會在哪裡？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629707392/blog/htmlPosition/relativeStartPoint_nsc1nk.png) ->->-> `會往左位移-value1`
<!--SR:!2022-10-03,17,248-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問要如何調整top、left、bottom、right值為正就往下，為負就往上![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-top-offset_qybhfg.png)->->-> `如果是調整top屬性的話，其屬性值value1若是正的話，就會將元素往下偏移；其屬性值若是負的話，就會將元素往上偏移。`
<!--SR:!2022-09-26,7,228-->


#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問要如何調整top、left、bottom、right值為正就往上，為負就往下 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-bottom-offset_x0jc6r.png)->->-> `如果是調整bottom屬性的話，其屬性值value1若是正的話，就會將元素往上偏移；其屬性值若是負的話，就會將元素往下偏移。`
<!--SR:!2022-10-25,30,248-->


#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問要如何調整top、left、bottom、right值為正就往左，為負就往右![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-right-offset_au8dxj.png)->->-> `如果是調整right屬性的話，其屬性值value1若是正的話，就會將元素往左偏移；其屬性值若是負的話，就會將元素往右偏移。`
<!--SR:!2022-09-29,14,248-->

#🧠 橘點是position: static的元素A開始渲染的起始點，黑點為設定relative的元素A，請問要如何調整top、left、bottom、right值為正就往右，為負就往左![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662565106/blog/htmlPosition/relative-direction/relative-left-offset_k59p4g.png) ->->-> `如果是調整left屬性的話，其屬性值value1若是正的話，就會將元素往右偏移；其屬性值若是負的話，就會將元素往左偏移。`
<!--SR:!2022-09-26,12,248-->


#🧠 在position：relative的元素下都設置著left、right這兩個屬性，請問會如何決定偏移值 ->->-> `會捨棄right這屬性，改選left為主`
<!--SR:!2022-10-19,28,250-->

#🧠 在position：relative的元素下都設置著top、bottom這兩個屬性，請問會如何決定偏移值 ->->-> `會捨棄bottom這屬性，改選top為主`
<!--SR:!2022-10-12,23,250-->

#🧠  在position：relative的元素下，top 和 bottom 中會挑選top的原因->->-> `採取normal flow所預設的排版方向，由上而下來排`
<!--SR:!2022-10-19,28,250-->

#🧠 在position：relative的元素下，left 和 right 中會挑選left的原因 ->->-> `採取normal flow所預設的排版方向，由左而右來排`
<!--SR:!2022-09-26,12,248-->

#🧠 在position：relative的元素下都設置著top、bottom、left、right這四種屬性，請問會如何決定偏移值(提示：以屬性共存來說) ->->-> `會選top和left這兩種屬性`
<!--SR:!2022-09-30,13,247-->


---
Status: 
Tags:
[[當元素的position屬性被調整成非static的屬性值，就能依據著top、left、right、bottom、z-index來調整其元素的位置]]
Links:
[[@mdnPositionCSSCascading]]
References:
