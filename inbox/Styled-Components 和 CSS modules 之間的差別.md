## 描述


### CSS-in-JS 
Styled-Components 是 CSS-in-JS 概念的實現；CSS modules 則不是CSS-in-JS概念的實現

### 元件樣式層面的渲染是否重複渲染

1. Styled-Components 由於是以JS角度將指定樣式內容寫進對應的Component ，所以只要觸發對應元件的渲染，都有可能間接讓styled-components元件重新解析樣式內容來決定最後對應內容

2. CSS modules 本身並不是將指定樣式內容寫進對應的Component，而是讓對應Component的實際DOM節點去採用對應生成的class selector，與Styled-Components相較，每次觸發對應元件的渲染，不會讓JS去解析樣式部分。

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References: