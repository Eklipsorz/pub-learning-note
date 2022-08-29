

## 描述

[[@mdnSpecificityCSSCascading]]
> Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. 
> 
> The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.





重點：
- 由於每個元件A下會有多個selector 來指定元件A要什麼樣的外表，多少會有發生衝突的屬性或者沒有發生衝突的屬性，沒發生衝突的屬性皆會合併成元件A會有的屬性，比如説 以下元件會有兩個selector指向它，分別是p和hightlight，這兩個selector所指定的屬性皆沒衝突，所以就直接合併。

`<P class="highlight">這個段落將被顯示為黃底紅字粗體。</P>`

```
例子：

p{
    font-size: 110%;
    font-family: garamond, sans-serif;
}
h2{
    color: red;
    background: white;
}
.highlight{
    color: red;
    background: yellow;
    font-weight: bold;
}
```
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661802724/blog/cssTag/css-merge-example_ms662h.png)

- 而若多個指向同個元件A的selector都有起衝突的屬性，如都指定color為什麼顏色，這時會採用Specificity算法
- Specificity 算法 則是在眾多selector指向同一個元件A的情況下，決定哪一個起衝突的/無法明確的declaration要被採用至元件A
### CSS declaration
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]

### Specificity 如何計算
[[@mdnSpecificityCSSCascading]]
> Specificity is an algorithm that calculates the weight that is applied to a given CSS declaration. The weight is determined by the number of selectors of each weight category in the selector matching the element (or pseudo-element). If there are two or more declarations providing different property values for the same element, the declaration value in the style block having the matching selector with the greatest algorithmic weight gets applied.

> The specificity algorithm is basically a three-column value of three categories or weights - ID, CLASS, and TYPE - corresponding to the three types of selectors. The value represents the count of selector components in each weight category and is written as ID - CLASS - TYPE. The three columns are created by counting the number of selector components for each selector weight category in the selectors that match the element.



重點：
- Specificity 是一種算法，主要會用權重來衡量每個
- 每一個declaration 會擁有三種欄位值來分別代表著同樣屬性名稱

### Specificity
specificity
> the quality of being specific 

specific
> clear and exact

重點：
- specific 是指清晰和正確
- specificity 是指清晰和正確的程度

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]
References:
[[@mdnSpecificityCSSCascading]]