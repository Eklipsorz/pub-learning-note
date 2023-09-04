## 描述


### label 元件
[[@mdnInputLabelElement]]
> \<label\>: The Input Label element
> The \<label\> HTML element represents a caption for an item in a user interface.

> The value of the for attribute must be a single id for a labelable form-related element in the same document as the \<label\> element. So, any given label element can be associated with only one form control.


重點：
- label 元素是用來顯示某個項目的標題
- label 的 for 屬性 會對應著 可被label綁定的表格元件A所擁有的id，以此讓label元件和元件A擁有互動上的關係，比如點擊label會自動讓使用者游標指向對應元件A的位置。


### React：label 的 for 屬性

[[@reactDOMElementsReact]]
> ### htmlFor
> React element 使用 `htmlFor` 來替代 `for`，因為 `for` 在 JavaScript 是保留字。

重點：
- 在定義react element的for屬性時，由於for本身是JS的保留字且react element是JS延伸語法，貿然使用會有衝突的可能，所以會用htmlFor來替代for屬性。

## 複習

#🧠 label 元素是用做什麼？ ->->-> `顯示某個項目的標題`
<!--SR:!2025-01-26,526,250-->

#🧠 label 元素的for屬性是什麼？用途？ ->->-> `會對應著 可被label綁定的表格元件A所擁有的id，以此讓label元件和元件A擁有互動上的關係`
<!--SR:!2025-01-20,524,250-->

#🧠 label 元素的for屬性是會對應著 可被label綁定的表格元件A所擁有的id，以此讓label元件和元件A擁有互動上的關係，請舉例有何種互動上的關係 ->->-> `點擊label會自動讓對應元件轉換成active element。`
<!--SR:!2023-07-28,190,250-->


#🧠 若要在React element 上定義for屬性，可直接定義for屬性嗎？為什麼 ->->-> `並不能，由於由於for本身是JS的保留字且react element是JS延伸語法，貿然使用會有衝突的可能`
<!--SR:!2024-11-21,479,250-->

#🧠 由於for本身是JS的保留字且react element是JS延伸語法，貿然使用會有衝突的可能，若要設定React element的屬性，可以有什麼解法 ->->-> `可以改以htmlFor屬性來定義`
<!--SR:!2023-12-20,107,230-->


---
Status: #🌱 
Tags:
[[React]] - [[HTML]]
Links:
References:
[[@mdnInputLabelElement]]
[[@reactDOMElementsReact]]