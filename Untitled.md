## 描述

> 很常你會遇到一種情況是，有好幾個獨立元件同時都跟某個資料狀態 (shared state) 的改變有相依性，React 建議的處理模式是，將這個資料狀態提升 (lifting state up) 到這些元件的某個共同父元件 (closest common ancestor) 上面。

> 實作概念是，當子元件事件 (Child Events) 發生時，透過父元件傳進來的 callback function 通知父元件有資料變動，然後由父元件統一計算得到新的父元件 state，然後透過 props 反應資料更新回這些子元件。


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: