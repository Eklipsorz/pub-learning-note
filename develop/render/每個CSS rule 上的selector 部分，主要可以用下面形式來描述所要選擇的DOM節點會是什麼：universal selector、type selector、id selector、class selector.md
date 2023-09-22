## 描述

每個CSS rule 上的selector 部分，主要可以用下面形式來描述所要選擇的DOM節點會是什麼：
- type 形式來選擇：type selector
- id 形式來選擇：id selector
- class 形式來選擇：class selector


### The universal selector
[[@mdnUniversalSelectorsCSS]]
> # Universal selectors
> The CSS **universal selector** (`*`) matches elements of any type.

```
/* Selects all elements */
* {
  color: green;
}
```

重點：
- universal selector 是用任意形式來選擇相符的DOM節點，換言之，可以指向任意DOM節點
- 形式會是用*
```
* {
  color: green;
}
```

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
- type selector 形式會是用DOM節點種類來命名，比如説
```
div {
	.....
}
```

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
- id selector 形式會是用#\<id\>來命名，其中\<id\>是特定識別字串，比如說
```
#demo {
  border: red 2px solid;
}
```

### class selector

[[@mdnClassSelectorsCSS]]
> Class selectors
>
> The CSS class selector matches elements based on the contents of their class attribute.
```
.spacious {
  margin: 2em;
}
```

重點：
- class selector 是用特定class名稱來選擇符合class名稱的DOM節點
- class selector 形式會是用.\<class\>來命名，其中\<class\>來表示特定類別，比如說：
```
.spacious {
  margin: 2em;
}
```
## 複習

#🧠 每個CSS rule 上的selector 部分，請舉例說明是哪四種形式可以描述所要選擇的DOM節點會是什麼 ->->-> `universal selector、type selector、id selector、class selector`
<!--SR:!2023-11-08,47,190-->

#🧠 每個CSS rule 上的selector 部分，universal selector、type selector、id selector、class selector主要是用來做什麼？ ->->-> `用四種形式來描述所要選擇的DOM節點會是什麼`
<!--SR:!2024-10-26,480,250-->

#🧠 type selector 是什麼樣的selector->->-> `type selector  是用DOM節點種類來選擇相符的DOM節點`
<!--SR:!2024-01-21,307,250-->

#🧠 id selector 是什麼樣的selector->->-> `id selector 是用特定id名稱來選擇擁有符合id名稱的DOM節點`
<!--SR:!2024-01-12,304,250-->

#🧠 universal selector 是什麼樣的selector ->->-> `是用任意形式來選擇相符的DOM節點`
<!--SR:!2025-03-08,563,250-->


#🧠 class selector 是什麼樣的selector ->->-> `class selector 是用特定class名稱來選擇符合class名稱的DOM節點`
<!--SR:!2024-02-06,318,250-->

#🧠 class selector 是用特定class名稱來選擇符合class名稱的DOM節點，請用程式碼來舉例 ->->-> `.demo { ... }`
<!--SR:!2024-10-08,469,250-->

#🧠 id selector 是用特定id名稱來選擇符合id名稱的DOM節點，請用程式碼來舉例形式 ->->-> `#demo { ... }`
<!--SR:!2024-04-07,230,230-->

#🧠 type selector 是用DOM節點種類來選擇相符的DOM節點，請用程式碼來舉例形式 ->->-> `div { ... }`
<!--SR:!2025-01-25,521,250-->

#🧠 universal selector 是用任意形式來選擇相符的DOM節點，請用程式碼舉例形式 ->->-> `* { ... }`
<!--SR:!2024-02-24,331,250-->

---
Status: #🌱 
Tags:
[[CSS]] - [[Rendering]]
Links:
[[id 是同一份DOM文件用來識別特定節點的識別字串，class是同一份DOM文件下用來將多個特定節點分成好幾類]]
References:
[[@mdnUniversalSelectorsCSS]]
[[@mdnIDSelectorsCSS]]
[[@mdnTypeSelectorsCSS]]
[[@mdnClassSelectorsCSS]]