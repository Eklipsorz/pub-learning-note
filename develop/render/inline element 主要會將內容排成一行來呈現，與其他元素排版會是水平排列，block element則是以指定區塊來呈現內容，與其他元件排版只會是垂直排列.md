## 描述


### 文獻：
[[@mdnBlocklevelElementsHTML]]
> A Block-level element occupies the entire horizontal space of its parent element (container), and vertical space equal to the height of its contents, thereby creating a "block".


[[@mdnInlineElementsHTML]]
> Inline elements are those which only occupy the space bounded by the tags defining the element, instead of breaking the flow of the content.

[[@mdnCSSFlowLayout]]
> _Normal Flow_, or Flow Layout, is the way that Block and Inline elements are displayed on a page before any changes are made to their layout. The flow is essentially a set of things that are all working together and know about each other in your layout. Once something is taken _out of flow_ it works independently.

> In normal flow, inline elements display in the inline direction, that is in the direction words are displayed in a sentence according to the Writing Mode of the document. Block elements display one after the other, as paragraphs do in the Writing Mode of that document. In English therefore, inline elements display one after the other, starting on the left, and block elements start at the top and move down the page.

### Flow Layout 



> 頁面流 (page flow)，也有人稱作佈局流 ([normal flow](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/normal_flow)) 或文字流，以下統稱頁面流。頁面流是指預設狀態下、還沒有設定任何 CSS 樣式時，網頁元素會遵循由左而右、由上而下的預設脈絡來排列、新增。下圖顏色由淺入深表示頁面流的流動脈絡：

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662568830/blog/htmlPosition/relative-direction/default-flow_twzmdl.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662568830/blog/htmlPosition/relative-direction/default-flow_twzmdl.png)

重點：
- flow layout 或者 normal flow 是系統預設對於元素的排版方式，預設會是由左而右、由上而下的預設排版策略來新增、排列

### inline element

該元件的內容主要會排成一行，且不會特別佔別據沒顯示內容的區塊而將元件和其他元件特別獨立開來，以此特性會讓該容器能夠與其他容器在同一行內呈現，而inline element就是由此而得名。


[[@ithomeHunXieErInlineblock]]
> -   除了`替換元素`之外，`無法`透過 `width` 與 `height` 屬性調整寬高。
> -   除了`替換元素`之外，寬高取決於內容(例如文字)的`長度`與`行高(line height)`。
> -   呈現`水平排列`。
> -   裡面只能放 inline 元素。


內部顯示(the inner display type)：會以inline element的容器來儲存和呈現內容
外部顯示(the outer display type)：與其他元素排版，會以水平排列為主


特點：
1. 除了replaced element以外，無法透過width和height屬性來調整寬高
2. 除了replaced element以外，元件的總高寬取決於元件內容的長度(寬度)和行高(高度)
3. 與其他元素排版：會以水平排列為主
4. 裡面只能放inline元素

  
### block element

該容器會以指定高寬度的區塊來存放內容，並且保持每一行只會有該區塊，所以呈現上會是新的一行來呈現，並不會與其他容器在同一行呈現。


[[@ithomeHunXieErInlineblock]]
> -   預設寬度為容器的 `100%`。
> -   `可以`透過 `width` 與 `height` 屬性調整寬高。
> -   強迫換行，呈現`垂直排列`。
> -   裡面可放 inline 元素或 block 元素。


內部顯示(the inner display type)：會以block element的容器來儲存和呈現內容
外部顯示(the outer display type)：與其他元素排版，會以垂直排列為主

特點：
1. 預設寬度為容器的100%
2. 可以透過width和height屬性調整高寬
3. 與其他元素排版：強迫換行，元素都會呈現垂直排列
4. 裡面可放inline元素和block元素


### replaced element
[[@mdnReplacedElementsCSS]]
> In CSS, a replaced element is an element whose representation is outside the scope of CSS; they're external objects whose representation is independent of the CSS formatting model.

> CSS 中所謂的「置換元素 (**Replaced element**)」，即是該元素所呈現的內容不在 CSS 的控制範圍之內。這類外部物件所呈現的內容均獨立於 CSS 之外，例如 \<img\>的內容是取決於 src 屬性

重點：
- replaced element 是一種元素，它本身只是特定呈現內容的連結資訊，其呈現內容本身獨立於CSS的排版方式，當瀏覽器渲染後，該元素就會利用連結資訊來抓取對應特定呈現內容來替代目前元素。
- 元素會是：
	- img
	- video

## 複習

#🧠 replaced element 是什麼？ ->->-> ` 是一種元素，它本身只是特定呈現內容的連結資訊，其呈現內容本身獨立於CSS的排版方式，當瀏覽器渲染後，該元素就會利用連結資訊來抓取對應特定呈現內容來替代目前元素`
<!--SR:!2023-12-02,103,230-->

#🧠 replaced element 會有哪些元件？ ->->-> `img、video`
<!--SR:!2025-02-05,534,250-->

#🧠 inline element 是什麼？ ->->-> `該元件的內容主要會排成一行，且不會特別佔別據沒顯示內容的區塊而將元件和其他元件特別獨立開來，以此特性會讓該容器能夠與其他容器在同一行內呈現，而inline element就是由此而得名`
<!--SR:!2023-12-04,101,230-->

#🧠 inline element 特點有哪些? (有四點，高寬、排列、存放什麼) ->->-> `除了replaced element以外，無法透過width和height屬性來調整寬高、除了replaced element以外，元件的總高寬取決於元件內容的長度(寬度)和行高(高度)、元件的元件呈現內容會以水平排列為主、裡面只能放inline元素`
<!--SR:!2023-12-04,102,230-->


#🧠 每個inline元素 與其他元素排版是如何？ ->->-> `水平排列`
<!--SR:!2023-12-03,104,230-->

#🧠 inline element 能放什麼元素 ->->-> `只能放inline元素`
<!--SR:!2024-09-25,456,250-->

#🧠  inline element 的高寬如何決定->->-> `高是由行高屬性決定、寬是由內容來決定`
<!--SR:!2023-11-22,89,230-->

#🧠 block element 是什麼？ ->->-> `該容器會以指定高寬度的區塊來存放內容，並且保持每一行只會有該區塊，所以呈現上會是新的一行來呈現，並不會與其他容器在同一行呈現。`
<!--SR:!2023-11-27,98,230-->

#🧠 block element 能放什麼元素？ ->->-> `裡面可放inline元素和block元素`
<!--SR:!2025-03-05,557,250-->

#🧠 每個 block element與其他元素排版是如何？ ->->-> ` 與其他元素排版：強迫換行，元素都會呈現垂直排列`
<!--SR:!2023-12-05,101,230-->

#🧠 block element 的高寬如何決定 ->->-> `可以透過width和height屬性調整高寬`
<!--SR:!2023-09-19,134,230-->

#🧠 block element的預設寬度為何？ ->->-> `為容器的100%`
<!--SR:!2025-02-06,535,250-->

#🧠 block element的特點有什麼？(有四點，大小、高寬、排列、存放什麼) ->->-> `1. 預設寬度為容器的100% 2. 可以透過width和height屬性調整高寬 3. 與其他元素排版：強迫換行，元素都會呈現垂直排列 4. 裡面可放inline元素和block元素`
<!--SR:!2023-11-22,88,230-->


#🧠 flow layout 是什麼？ ->->-> `系統預設對於元素的排版方式`
<!--SR:!2024-09-29,454,250-->

#🧠 normal flow 是什麼？ 和flow layout 有什麼差別->->-> `系統預設對於元素的排版方式`
<!--SR:!2025-02-18,549,250-->

#🧠 flow layout 或者 normal flow 是系統預設對於元素的排版方式，預設會如何排？ ->->-> `預設會是由左而右、由上而下的預設排版策略來新增、排列`
<!--SR:!2025-03-02,559,250-->

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
[[@ithomeHunXieErInlineblock]]
[[@mdnReplacedElementsCSS]]