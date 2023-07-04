## 描述

[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]

由於JSX 侷限而得採用wrapper component和array，其中array得要一直填寫key值才會減少不必要的誤判，這樣會使得開發上變得較為不方便，所以通常會採取前者，但採用前者的話，可能會是一直拿div或者其他元件來當wrapper element ，這會促使產生深度高到一定程度的div巢狀結構

```
<div>
   <div>
        <div>
            <div>
                ......
            </div>
        </div>
   </div>
</div>
```
  

> In bigger apps, you can easily end up with tons of unnecessary \<div\>s (or other elements)  which add no semantic meaning or structure to the page but are only there of React’s JSX requirement


然而，不一定是所有div都是必要的，大部分只是為了解決JSX問題，比如div 目前所在並不會帶來特別語義或者結構


### 帶來的問題
>if you have a wrapping div somewhere and you use nested CSS selectors

過多的div 會造成：
1.  div 的增長有可能會破壞原有CSS 樣式選擇器所選擇的DOM節點
2.  會讓瀏覽器渲染出不必要出現的HTML元素，甚至影響處理效率，比如每次渲染都會以深度有一定程度巢狀的div結構來重新渲染


## 複習

#🧠 由於JSX 侷限而採用wrapper element 和 array 來解決，這兩者會有什麼樣問題？->->-> `前者會促使產生不必要的div元件或者wrapper element來包含，甚至產生深度高到一定程度的div巢狀結構，array得要一直填寫key值才會減少不必要的誤判，這樣會使得開發上變得較為不方便`
<!--SR:!2023-05-30,161,250-->

#🧠 由於JSX 侷限而採用wrapper component，具體的wrapper component 通常會是拿什麼包含子節點(不考慮假的wrapper component) ->->-> `div元件`
<!--SR:!2023-06-07,154,230-->

#🧠 由於JSX 侷限而採用wrapper componentn所帶來的潛在問題是什麼？ ->->-> `div 的增長有可能會破壞原有CSS 樣式選擇器所選擇的DOM節點、會讓瀏覽器渲染出不必要出現的HTML元素，甚至影響處理效率，比如每次渲染都會以深度有一定程度巢狀的div結構來重新渲染`
<!--SR:!2023-07-02,182,250-->

#🧠 因JSX 侷限而採用wrapper element，那麼產生出來的wrapper element都是必要的嗎？為什麼？->->-> `不一定是所有div都是必要的，大部分只是為了解決JSX問題，比如div 目前所在並不會帶來特別語義或者結構`
<!--SR:!2023-05-29,160,250-->

#🧠 JSX 侷限而採用wrapper element 所產生出的巢狀結構會是什麼？用程式碼表示 ->->-> `![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815053/blog/react/react-element/div-hell_khxdhw.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815053/blog/react/react-element/div-hell_khxdhw.png)`
<!--SR:!2024-09-21,445,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]
References: