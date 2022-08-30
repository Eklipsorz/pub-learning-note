

## 描述

[[@mdnSpecificityCSSCascading]]
> Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. 
> 
> The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.





重點：
- Specificity 算法 是在眾多selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突。
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
### CSS declaration
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]

### Specificity 如何計算
[[@mdnSpecificityCSSCascading]]
> Specificity is an algorithm that calculates the weight that is applied to a given CSS declaration. The weight is determined by the number of selectors of each weight category in the selector matching the element (or pseudo-element). If there are two or more declarations providing different property values for the same element, the declaration value in the style block having the matching selector with the greatest algorithmic weight gets applied.

> The specificity algorithm is basically a three-column value of three categories or weights - ID, CLASS, and TYPE - corresponding to the three types of selectors. The value represents the count of selector components in each weight category and is written as ID - CLASS - TYPE. The three columns are created by counting the number of selector components for each selector weight category in the selectors that match the element.



重點：
- Specificity 是一種算法，主要會用權重來衡量每個declaration 
- 每一個declaration的權重是使用三種欄位值來表示，分別為如下，主要會依據著declaration所在的selector 是用什麼形式來表示
	- id : class : type
	- id 表示目前declaration 所在的 selector 有使用 id 來描述 selector 的具體程度，會用數字表示
	- class 表示目前declaration 所在的 selector 有使用 class 來描述 selector 的具體程度，會用數字表示
	- type 表示目前declaration 所在的 selector 有使用 type 來描述 selector 的具體程度，會用數字表示

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
<!--SR:!2022-09-02,3,250-->

---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]
References:
[[@mdnSpecificityCSSCascading]]