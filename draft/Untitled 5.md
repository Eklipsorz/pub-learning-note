

### position 屬性值



```
position: static | relative | absolute | fixed
top: value
bottom: value
left: value
right: value
```

  


  

  
  
  
  

5. 若position 設定為absolute時，其容器大小會跟著內容而變化，而定位方式會從static改變，且以離該元素最近的定位父元素(ancestor element，其position被設定static以外的值)所擁有定為參考點為基準點(圖中橘點)來定位，而定位方式是以該元素邊界和父元素邊界在父元素內部之間的距離作為基準點來調整top、bottom、left、right，類似於position: fixed的定位方式，只是差別在於還會挑有定位過的父元素，若一直都找不到合適的父元素(ancestor element)的話，才會以body/viewport邊界和其元素邊界之差來呈現。

  

(原文： is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport.) However, if an absolute positioned element has no positioned ancestor, it uses the document body, and move along with page scrolling.)

  

其top、bottom、left、right的移動方式會如同設定fixed那樣去決定元素的定位。

  

5. 若position設定為sticky，其容器大小並不會跟著內容而變化，而定位方式會從static改變，根據設定sticky的元素邊界與離他最近的scrolling ancestor(帶有scrolling 機制或者帶有捲軸元素的父元件)之間的邊界之間的距離(如圖中的value2)是否小於門檻值來變動元件的特性，其門檻值會以top、bottom、left、right的任一值為主，會優先以top值為門檻值(threshold)：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629787015/blog/htmlPosition/stickyPosition_kxapar.png)

  

若距離小於門檻值的話，設定sticky的元素會以fixed形式固定與scrolling ancestor之邊界保持threshold的距離：

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629787535/blog/htmlPosition/sticky2Fixed_uhhon4.png)

  

反之，若大於大於門檻值，其設定sticky的元素會以relative形式，且不會受到top、bottom、left、right而更動定位。另外若sticky元素真的找不到scrolling ancestor的話，會以body作為替代，因為body元素本身就帶有scrolling機制。

  

note:

1. Page Flow/Normal Flow: Flow是指放置內容的方向，而這裡Page Flow是指還沒套用任何CSS樣式的預設HTML放置內容之方向，其方向會是先由上而下來放，再來就從左至右。

  

2. Viewport (可視區): 是使用者能夠在網頁看到的全部區域(is the user's visible area of a web page)

  

3. 定位參考點：元素本身放置其他位置的基準點，通常元素會以自身的左上角作為定位參考點：圖中的黑點就是元素的定位參考點，當要位移該元素時，會以那個點來移動，並連帶移動整個元素，該定位參考點適用於position: relative，其餘position模式下皆不適用。

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629706579/blog/htmlPosition/positioningPoint_edkots.png)

  
  

4. position: static vs. relative vs. absolute vs. fixed

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1629726945/blog/htmlPosition/strengthOf4PositionsFromAC_xgtx7o.png)

  

  

6. 當一個元件設定自己的overflow屬性為hidden、scroll、auto、overlay時，便會被系統當成是scolling element。而overflow屬性是定義元素內容超過呈現範圍時該如何呈現。


## 複習