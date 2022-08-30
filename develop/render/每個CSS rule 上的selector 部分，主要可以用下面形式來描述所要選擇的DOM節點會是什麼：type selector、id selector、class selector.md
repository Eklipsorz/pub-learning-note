## 描述

每個CSS rule 上的selector 部分，主要可以用下面形式來描述所要選擇的DOM節點會是什麼：
- type 形式來選擇：type selector
- id 形式來選擇：id selector
- class 形式來選擇：class selector

### type selector 
[[@mdnTypeSelectorsCSS]]
> # Type selectors
>
> The CSS **type selector** matches elements by node name. In other words, it selects all elements of the given type within a document.

```
/* All <a> elements. */
a {
  color: red;
}
```

重點：
- type selector  是用DOM節點種類來選擇相符的DOM節點

### id selector

[[@mdnIDSelectorsCSS]]
> # ID selectors
>
> The CSS ID selector matches an element based on the value of the element's id attribute. In order for the element to be selected, its id attribute must match exactly the value given in the selector.

```
/* The element with id="demo" */
#demo {
  border: red 2px solid;
}
```

重點：
- id selector 是用特定id名稱來選擇擁有符合id名稱的DOM節點

### class selector

[[@mdnClassSelectorsCSS]]
> Class selectors
>
> The CSS class selector matches elements based on the contents of their class attribute.

重點：
- class selector 是用特定class名稱來選擇符合class名稱的DOM節點

## 複習

#🧠 每個CSS rule 上的selector 部分，主要可以用三種形式來描述所要選擇的DOM節點會是什麼 ->->-> `type selector、id selector、class selector`

#🧠 每個CSS rule 上的selector 部分，type selector、id selector、class selector主要是用來做什麼？ ->->-> `用三種形式來描述所要選擇的DOM節點會是什麼`

#🧠 type selector 是什麼樣的selector->->-> `type selector  是用DOM節點種類來選擇相符的DOM節點`
#🧠 id selector 是什麼樣的selector->->-> `id selector 是用特定id名稱來選擇擁有符合id名稱的DOM節點`
#🧠 class selector 是什麼樣的selector ->->-> `class selector 是用特定class名稱來選擇符合class名稱的DOM節點`


---
Status: #🌱 
Tags:
[[CSS]] - [[Rendering]]
Links:
[[id 是同一份DOM文件用來識別特定節點的識別字串，class是同一份DOM文件下用來將多個特定節點分成好幾類]]
References:
[[@mdnIDSelectorsCSS]]
[[@mdnTypeSelectorsCSS]]
[[@mdnClassSelectorsCSS]]