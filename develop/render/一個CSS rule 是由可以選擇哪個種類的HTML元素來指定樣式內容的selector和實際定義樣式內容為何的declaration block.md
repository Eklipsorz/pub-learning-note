


## 描述

[[@w3schoolCSSSyntax]]
> A CSS rule consists of a selector and a declaration block.


> The selector points to the HTML element you want to style.
>
> The declaration block contains one or more declarations separated by semicolons.
> 
> Each declaration includes a CSS property name and a value, separated by a colon.
> 
> Multiple CSS declarations are separated with semicolons, and declaration blocks are surrounded by curly braces.

![](https://www.w3schools.com/css/img_selector.gif)



[[@mdnCSSJiBenXueXiGaiRuHeKaiFa]]
> 整個架構我們稱為規則集 **(rule set)，或是簡稱為規則 (rule)** 也可以。（也注意名字裡面的單獨部分）

> 選擇器（Selector）

> 在這個規則的最前頭為 HTML 的元素名。它將決定你 HTML 裡什麼元素將被你接下來的設定影響（在這個範例中,就是 段落元素 `p`）。若要改變欲影響的元素，只要更改選擇器就行了。

> 宣告（Declaration）
> 單一個規則，例如 `color: red;` 指定了這個元素的呈現樣貌。

> 屬性 (Properties)
> 修改屬性是改變你 HTML 元素的一種方法 . (在這範例中, `color` 是段落（`p`）元素的一種屬性.) 在 CSS 中, 你可以選擇哪些屬性用來影響 rule.

> 屬性值 (Property value)
> **屬性值** 就是位於屬性右邊，在冒號（`:`）之後，從眾多的可能樣式選出一個給予屬性（範例中就是從眾多的 `color` 樣式中選出 `red`）

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/css-declaration-small.png)


重點：
- CSS rule set 是由多個 CSS rule所組成
- 每個CSS rule 是由一個selector和一個declaration block所構成。
- CSS rule 主要用作定義選擇到的HTML 元素會有什麼樣的樣式內容
- selector 部分是用來選擇哪個種類的HTML 元素或者HTML DOM節點
- 一個 declaration 是由一個屬性名稱(property)、屬性值(property value)、分號(;)，比如說color是屬性名稱、red是屬性值，屬性名稱和屬性值之間會有:，最後再來是分號
```
color: red;
```
- 同個選擇器內的所有declaration 會構成一個declaration block
- property 和 property value 是則是實際指定DOM元素會有什麼外表設定


### selector 命名緣由
> a device that allows you to choose something

重點：
- 一個可允許選擇特定內容的裝置

###  style 命名緣由
> to shape or design something such as a person's hair or an object like a piece of clothing or furniture, especially so that it looks attractive

重點：
- 對特定事物的外表進行塑形、設計以便使該事物更有吸引力
## 複習

#🧠 selector 命名緣由 ->->-> `一個可允許選擇特定內容的裝置`
<!--SR:!2023-12-23,291,250-->

#🧠   style 作為動詞的命名緣由為何？ ->->-> ` 對特定事物的外表進行塑形、設計以便使該事物更有吸引力`
<!--SR:!2023-12-22,293,248-->

#🧠 CSS rule set 是由什麼所組成的？->->-> `由多個CSS rule所組成的`
<!--SR:!2023-10-21,121,210-->

#🧠 每個CSS rule 是由什麼所組成的？ ->->-> `每個CSS rule 是由一個selector和一個declaration block所構成`
<!--SR:!2023-12-09,107,230-->

#🧠 每個CSS rule主要做啥？ ->->-> `定義選擇到的HTML元素會有什麼樣的樣式內容`
<!--SR:!2023-12-02,280,248-->

#🧠  每個CSS rule 是由一個selector和一個declaration block所構成，那麼selector是什麼？->->-> `主要用來選擇哪個種類的HTML元素或者HTML DOM節點`
<!--SR:!2024-09-10,446,250-->

#🧠  每個CSS rule 是由一個selector和一個declaration block所構成，那麼一個declaration block 是什麼？->->-> `由同一個selector下的所有declaration所組成`
<!--SR:!2024-12-03,470,230-->

#🧠 每個CSS rule 是由一個selector和一個declaration block所構成，那麼一個declaration  是什麼？ ->->-> `主要是以樣式屬性(property)、屬性值、分號(;)來組成`
<!--SR:!2023-12-11,112,228-->

#🧠 每個CSS rule 是由一個selector和一個declaration block所構成，那麼一個declaration  用途為？->->-> `定義selector所選擇的DOM節點會有什麼樣樣式屬性`
<!--SR:!2023-12-29,294,250-->

#🧠 請用程式碼來表示一個表示會有文字顏色為紅色、字體大小為24px的css rule該如何定義？ 並選定哪些是selector、declaration、property、property。->->-> ``
<!--SR:!2023-12-17,112,228-->

#🧠 請問這兩個color: red 和 color: red; 中，哪一個才是合法的CSS declaration? ->->-> `color: red; `
<!--SR:!2023-12-11,285,248-->



---
Status: #🌱 
Tags:
[[CSS]]
Links:
References:
[[@w3schoolCSSSyntax]]
[[@mdnCSSJiBenXueXiGaiRuHeKaiFa]]