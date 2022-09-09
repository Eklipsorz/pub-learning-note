## 描述

[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]

由於JSX 侷限而採用wrapper element和array，其中array得要一直填寫key值才會減少不必要的誤判，所以通常會採取前者，但採用前者的話，可能會是一直拿div或者其他元件來當wrapper element ，這會促使產生深度高到一定程度的div巢狀結構

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


然而，不一定是所有div都是必要的，比如div 目前所在並不會帶來特別語義或者結構，只是為了解決JSX侷限問題


### 帶來的問題
>if you have a wrapping div somewhere and you use nested CSS selectors

過多的div 會造成：
1.  div 的增長有可能會破壞原有CSS 樣式選擇器所選擇的DOM節點
2.  會讓瀏覽器渲染出不必要出現的HTML元素，甚至影響處理效率，比如每次渲染都會以深度有一定程度巢狀的div結構來重新渲染


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]
References: