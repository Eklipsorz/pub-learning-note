


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


---
Status: #🌱 
Tags:
[[CSS]]
Links:
References:
[[@w3schoolCSSSyntax]]
[[@mdnCSSJiBenXueXiGaiRuHeKaiFa]]