

## 描述

[[@mdnSpecificityCSSCascading]]
> Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. 
> 
> The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.





重點：
- 由於每個元件A下會有多個selector 來指定元件A要什麼樣的外表，所以必須要有算法去從中選一個selector來表明元件A要什麼樣的外表 或者 在眾多selector中，哪一個declaration應該要被採用至元件A
- Specificity 算法 則是在眾多selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A
### CSS declaration
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]

### Specificity 如何計算
[[@mdnSpecificityCSSCascading]]
> Specificity is an algorithm that calculates the weight that is applied to a given CSS declaration. The weight is determined by the number of selectors of each weight category in the selector matching the element (or pseudo-element). If there are two or more declarations providing different property values for the same element, the declaration value in the style block having the matching selector with the greatest algorithmic weight gets applied.

> The specificity algorithm is basically a three-column value of three categories or weights - ID, CLASS, and TYPE - corresponding to the three types of selectors. The value represents the count of selector components in each weight category and is written as ID - CLASS - TYPE. The three columns are created by counting the number of selector components for each selector weight category in the selectors that match the element.



重點：
- Specificity 是一種算法，主要會用權重
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