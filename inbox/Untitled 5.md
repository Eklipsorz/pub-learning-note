## 描述
[[@ithomeHunXieErInlineblock]]
> The display property defines an element’s display type, which consists of the two basic qualities of how an element generates boxes:

> -   the inner display type, which defines (if it is a non-replaced element) the kind of formatting context it generates, dictating how its descendant boxes are laid out. (The inner display of a replaced element is outside the scope of CSS.)
> -   the outer display type, which dictates how the principal box itself participates in flow layout.


> 簡單來說
> display 屬性用來決定元素的顯示方式，其中又分為：
> - 內部顯示：定義元素(替換元素除外）會形成何種格式化上下文，會影響後裔元素的佈局。
> - 外部顯示：定義元素本身如何參與佈局(layout)。


### display: inline-block

> 簡單來說，若將元素 A 的 display 值設定為 inline-block：
>
> 內部顯示：A 元素形成一個 塊格式化上下文(BFC)，對後裔元素來說是個 block 容器。

> 外部顯示：A 元素成為 行內級元素(inline-level element)，參與行內格式化上下文(IFC)，呈現水平排列。


![](https://i.imgur.com/8a7zMjs.png)

> -   `可以`透過 `width` 與 `height` 屬性調整寬高。
> -   呈現`水平`排列。
> -   在無設定 width 與 height 時，寬高由內容決定。
> -   裡面可放 inline 元素或 block 元素。



## 複習


---
Status: #🌱 
Tags:
[[HTML]] - [[CSS]]
Links:
[[box-sizing 屬性是設定以哪個盒子的總高寬來當作元素的width、height這兩個屬性]]
[[inline element 主要會將內容排成一行來呈現，與其他元素排版會是水平排列，block element則是以指定區塊來呈現內容，與其他元件排版只會是垂直排列]]

References:
[[@ithomeHunXieErInlineblock]]