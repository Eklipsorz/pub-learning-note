## 描述
[[@ithomeHunXieErInlineblock]]
> The display property defines an element’s display type, which consists of the two basic qualities of how an element generates boxes:

> -   the inner display type, which defines (if it is a non-replaced element) the kind of formatting context it generates, dictating how its descendant boxes are laid out. (The inner display of a replaced element is outside the scope of CSS.)
> -   the outer display type, which dictates how the principal box itself participates in flow layout.


> 簡單來說
> display 屬性用來決定元素的顯示方式，其中又分為：
> - 內部顯示：定義元素(替換元素除外）會形成何種格式化上下文，會影響後裔元素的佈局。
> - 外部顯示：定義元素本身如何參與佈局(layout)。

重點：
- display 屬性定義元件呈現的方式，包含了：
	- inner display type：定義元件內部呈現的方式是如何以及元件所包含的子元件之間的排版呈現。
	- outer display type：定義元件本身如何與其他元件進行排版呈現。


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

重點：
- display: inline-block 元件是指定其元件的inner display type和outer display type分別：
	- inner display type 是以block形式來呈現內容和包含的子元件
	- outer display type 是以inline特有的方式-水平排列來與其他元件排列
- 特點：
	- 元件本身可以透過width和height這兩種屬性來調整寬高
	- 元件本身和其他元件之間的排版呈現是以水平排列
	- 若沒設定width、height，寬高由內容決定
	- 裡面可放inline元素或者block元素

## 複習

#🧠 display 屬性是什麼？ ->->-> `定義元件呈現的方式`
<!--SR:!2023-05-09,150,250-->

#🧠  display 屬性定義元件呈現的方式，包含了？ ->->-> `inner display type：定義元件內部呈現的方式是如何以及元件所包含的子元件之間的排版呈現、outer display type：定義元件本身如何與其他元件進行排版呈現`
<!--SR:!2023-07-01,186,250-->


#🧠 display 屬性定義元件呈現的方式，inner display type是什麼？ ->->-> `定義元件內部呈現的方式是如何以及元件所包含的子元件之間的排版呈現。`
<!--SR:!2023-07-02,186,250-->


#🧠 display 屬性定義元件呈現的方式，outer display type是什麼？ ->->-> `定義元件本身如何與其他元件進行排版呈現。`
<!--SR:!2023-07-05,188,250-->

#🧠 display: inline-block 是指定元件會是什麼？->->-> `是指定其元件的inner display type和outer display type分別： inner display type 是以block形式來呈現內容和包含的子元件和outer display type 是以inline特有的方式-水平排列來與其他元件排列`
<!--SR:!2023-01-26,34,230-->

#🧠 display: inline-block 的元件本身的高寬如何決定？->->-> `可以透過width和height這兩種屬性來調整寬高`
<!--SR:!2023-01-15,34,230-->

#🧠 display: inline-block 的元件本身的高寬如何決定？若沒設定width和height這屬性 ->->-> `寬高由內容決定`
<!--SR:!2023-07-13,194,250-->

#🧠 display: inline-block 的元件與其他元件的排版呈現是如何？->->-> `是以水平排列`
<!--SR:!2023-02-09,40,230-->

#🧠 display: inline-block 的元件可以存放什麼元件？ ->->-> `裡面可放inline元素或者block元素`
<!--SR:!2023-07-11,192,250-->

#🧠 display: inline-block 的元件 所擁有的特點是什麼(有四點，高寬、沒設定高寬、排列、存放) ->->-> `	- 元件本身可以透過width和height這兩種屬性來調整寬高 - 元件本身和其他元件之間的排版呈現是以水平排列 - 若沒設定width、height，寬高由內容決定 - 裡面可放inline元素或者block元素`
<!--SR:!2023-02-03,38,230-->



---
Status: #🌱 
Tags:
[[HTML]] - [[CSS]]
Links:
[[box-sizing 屬性是設定以哪個盒子的總高寬來當作元素的width、height這兩個屬性]]
[[inline element 主要會將內容排成一行來呈現，與其他元素排版會是水平排列，block element則是以指定區塊來呈現內容，與其他元件排版只會是垂直排列]]
References:
[[@ithomeHunXieErInlineblock]]