## 描述



### Event Flow

如果使用者對著巢狀結構下的子元件來進行互動時，比如類似於程式碼中的元素3(element3)，那麼瀏覽器該如何判定這次的互動/事件是屬於哪個元素呢？瀏覽器大可直接根據事件是源自於哪裡來將事件歸類於element3，並且由它的事件處理來處理

```
<element1>
	<element2>
		<element3>content</element3>
	</element2>
</element1>
```

  

可由於是巢狀關係(如下圖)，元素3(element3)被元素2(element2)所包含著，而元素2(element2)被元素1(element1)包含著，嚴格來說，當使用者對元素3(element3)做互動，同樣地也對著另外兩個元素進行互動，更甚至說包含這些元素的元素(比如body)也跟著互動。


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630587482/blog/event/threeElements_lohr6c.png)

  
  

這時，瀏覽器可以有幾種選擇去決定事件是屬於哪個元件，第一種選擇是按照之前的規則，直接將事件歸類於元素3(element3)並發送信號給元素3，並對元素3的EventListener來找尋對應的事件處理，另外一種則是使用事件流(event flow)將訊號傳遞給每個包含元素3的元素，並試著對這些元素的EventListener找尋對應的事件處理，只是傳遞方向又可以細分兩種，一種是從最外圍的元素1開始往內傳遞的事件捕獲(event capture)，也就是信號會先傳遞至元素1，接著在傳遞元素2，最後傳遞元素3，另外一種則是從元素3往外傳遞信號的事件冒泡(Event bubbling)，也就是信號會先傳遞至元素3(發生事件的來源處)，接著在傳遞至元素2，最後傳遞元素1。

  

不過實際上來說，瀏覽器傳遞信號會一次分三種階段來傳遞信號，當對一個目標元件X產生互動時，第一個階段會先從包含元件X的最外面元件到內部元件來傳遞信號的捕獲階段(Capturing Phase)，第二個階段為從目標元件X的父元件傳遞信號至目標元件X的目標階段(Target Phase)，最後一個階段會先從目標元件X往外傳遞信號的冒泡階段(Bubbling Phase)，當使用者對某個元件X進行互動時，瀏覽器會先透過第一個階段來傳遞信號，接著就是第二個階段：將信號傳遞至實際發生事件/互動的元件X，最後就是第三個階段傳遞信號。

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1636879992/blog/event/currentPropagationPath_rj9x5j.png)

## 複習

---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
[[在event flow中，每個接收到事件訊號的DOM節點會先接收信號並做對應事件處理完畢之後才會發送信號至下一個DOM節點]]
[[arrow function 在implicit binding、explicit binding、addEventListener上的案例]]
References: