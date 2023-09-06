## 描述

[[@mdnBoxModelLearn]]

> What is the CSS box model?
>
> The CSS box model as a whole applies to block boxes and defines how the different parts of a box — margin, border, padding, and content — work together to create a box that you can see on a page. Inline boxes use just some of the behavior defined in the box model.
>
> To add complexity, there is a standard and an alternate box model. By default, browsers use the standard box model.


>Parts of a box
> Making up a block box in CSS we have the:
>
>Content box: The area where your content is displayed; size it using properties like inline-size and block-size or width and height.
>
> Padding box: The padding sits around the content as white space; size it using padding and related properties.
>
> Border box: The border box wraps the content and any padding; size it using border and related properties.
   > 
>Margin box: The margin is the outermost layer, wrapping the content, padding, and border as whitespace between this box and other elements; size it using margin and related properties.

> The below diagram shows these layers:

![](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662472122/blog/css/box-model/box-model-outline_bamp7e.png)


重點：
- 每一個HTML 元素在渲染層面上是以 CSS box model來構成
- CSS Box Model：是由多種Box組合在一起的結構，這些盒子都負責裝載特定內容，分別有：
	- Content Box：裝載HTML 元素的主要內容
		- Box 本身(不算裝載)高寬會分別由height、width來決定
	- Padding Box：如其名，本身裝載Content Box內容
		- Box 本身(不算裝載)高寬分別由padding-top、padding-bottom、padding-left、padding-right來決定
	- Border Box ：本身負責裝載著Padding Box內容
		- Box 本身(不算裝載)高寬分別由border-top、border-bottom、border-left、border-right來決定
	- Margin Box：本身負責裝載著Border Box內容
		- Box 本身(不算裝載)高寬分別由Margin-top、Margin-bottom、Margin-left、Margin-right來決定





### padding 命名緣由

> is soft material which is put on something or inside it in order to make it less hard, to protect it, or to give it a different shape. 

重點：
- padding 一種放在盒子中的軟性填充物，專門包覆特定事物不受到破壞

### margin 命名緣由

> the outer edge of an area

重點：
- 一個區域的外邊緣


## 複習

#🧠 padding 命名緣由 ->->-> `padding 一種放在盒子中的軟性填充物，專門包覆特定事物不受到破壞`
<!--SR:!2024-01-30,313,250-->

#🧠 margin 命名緣由 ->->-> `一個區域的外邊緣`
<!--SR:!2025-01-22,503,230-->

#🧠 每一個HTML元素在CSS上會被當成是什麼？ ->->-> `CSS box model`
<!--SR:!2023-12-03,100,229-->


#🧠 CSS Box Model 是什麼結構？ ->->-> `是由多種Box組合在一起的結構，這些盒子都負責裝載特定內容，分別有Content Box、Padding Box、Border Box、Margin Box`
<!--SR:!2023-12-08,106,230-->

#🧠 在CSS Box Model，Content Box 是什麼？ ->->-> `裝載HTML 元素的主要內容`
<!--SR:!2023-11-19,264,250-->


#🧠 預設下，CSS Box Model，Content Box 本身的大小屬性由什麼決定？ ->->-> `width、height`
<!--SR:!2023-11-06,132,210-->


#🧠 在CSS Box Model，Padding Box 是什麼？ ->->-> `如其名，本身裝載Content Box內容`
<!--SR:!2025-02-14,545,250-->


#🧠 在CSS Box Model，Padding Box  本身的大小屬性由什麼決定？ ->->-> `Box 本身(不算裝載)高寬分別由padding-top、padding-bottom、padding-left、padding-right來決定`
<!--SR:!2024-01-31,314,250-->


#🧠 在CSS Box Model，Border Box 是什麼？ ->->-> `本身負責裝載著Padding Box內容`
<!--SR:!2025-02-07,536,250-->


#🧠 在CSS Box Model，Border Box  本身的大小屬性由什麼決定？ ->->-> `Box 本身(不算裝載)高寬分別由border-top、border-bottom、border-left、border-right來決定`
<!--SR:!2023-12-01,98,230-->

#🧠 在CSS Box Model，Margin Box 是什麼？ ->->-> `本身負責裝載著Border Box內容`
<!--SR:!2024-02-09,315,250-->


#🧠 在CSS Box Model， Margin Box  本身的大小屬性由什麼決定？ ->->-> `Box 本身(不算裝載)高寬分別由Margin-top、Margin-bottom、Margin-left、Margin-right來決定`
<!--SR:!2025-02-17,546,250-->

#🧠 Box Model用這個例子來說明盒子有哪些？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662475900/blog/css/box-model/box-model-question_abqeis.png) ->->-> ``
<!--SR:!2023-12-07,103,230-->



---
Status: #🌱 
Tags:
[[HTML]] - [[CSS]]
Links:
References:
[[@mdnBoxModelLearn]]