## 描述


### 文獻：
[[@mdnBlocklevelElementsHTML]]
> A Block-level element occupies the entire horizontal space of its parent element (container), and vertical space equal to the height of its contents, thereby creating a "block".


[[@mdnInlineElementsHTML]]
> Inline elements are those which only occupy the space bounded by the tags defining the element, instead of breaking the flow of the content.

[[@mdnCSSFlowLayout]]
> In normal flow, inline elements display in the inline direction, that is in the direction words are displayed in a sentence according to the Writing Mode of the document. Block elements display one after the other, as paragraphs do in the Writing Mode of that document. In English therefore, inline elements display one after the other, starting on the left, and block elements start at the top and move down the page.


## inline element

容器會以實際容器所存的內容為主且不會特別佔據沒顯示內容的區塊而將容器特別獨立開來，以此特性會讓該容器能夠與其他容器在同一行內呈現，而inline element就是由此而得名。

  
  

特點：

1. 容器的範圍會貼齊實際內容，也就是說容器內並不會出現額外的空白

2. 容器會以內容為主，並不能夠隨意調整高度和寬度

3. 容器在網頁上的呈現並不會在新的一行呈現，會貼齊上個容器後

  
  

## block element

該容器會以特定的高寬度來製作以及使用足夠大的margin來與其他容器隔開來，這並不像inline那樣會貼齊內容製作，所以容器內部本身會夾雜著除了主要內容以外的空白，且本身會用margin來隔開其他容器，所以會呈現上會是新的一行來呈現，並不會與其他容器在同一行呈現。

  

特點：

1. 容器的範圍並不會貼齊實際內容，也就是說容器內很有可能會出現額外的空白

2. 容器可以隨意調整高度和寬度

3. 容器在網頁上的呈現會在新的一行出現，並不會貼齊上個容器後

  
  
  


## 複習


---
Status: #🌱 
Tags:
[[CSS]] - [[HTML]]
Links:
[[box-sizing 屬性是設定以哪個盒子的總高寬來當作元素的width、height這兩個屬性]]
[[每一個HTML 元素都是由多種盒子相互裝載而成的結構，該結構稱之為Box Model]]
References:
[[@DifferenceBlockElements2021]]
[[@freecodecampInlineElementsBlock]]
[[@mdnBlocklevelElementsHTML]]
[[@mdnInlineElementsHTML]]
[[@mdnCSSFlowLayout]]