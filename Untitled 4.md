## 描述
除了DOM以外，還有一種是為了能與瀏覽器本身進行互動的樹狀結構的模型-Browser Object Model，在DOM的基礎下將瀏覽器本身視為一個物件來允許其他語法與它互動，在這個模型下，其根節點是瀏覽器本身(window)，其子節點有DOM根節點-document、frames、history、location、screen，其中document節點子節點會接續著DOM剩下的內容。

  

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1630066487/blog/dom/bomHierarchy_kp1icw.png)

  

然而W3C還未對BOM進行嚴格的規範，基本上瀏覽器對於BOM的實現會有不一致的問題，不過大部分瀏覽器都支援BOM和DOM這兩套模型，當如果要調用DOM的節點時，可以不必從BOM的根節點開始調用，直接從DOM根節點就可以實現了，然而當要調用BOM的節點時，就必須直接從BOM根節點開始進行。


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: