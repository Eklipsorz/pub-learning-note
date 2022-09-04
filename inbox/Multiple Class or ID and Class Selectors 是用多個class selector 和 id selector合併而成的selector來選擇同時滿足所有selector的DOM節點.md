## 描述

> ### Combinations of Classes and IDs
> The big point here is that you can target elements that have combinations of classes and IDs by stringing those selectors together without spaces.


> #### ID and Class Selector
> As we covered above, you can target elements by a combination of ID and class.

```html
<h1 id="one" class="two">This Should Be Red</h1>
```

```css
#one.two { color: red; }
```

> #### Double Class Selector

> Target an element that has all of multiple classes. Shown below with two classes, but not limited to two.

```html
<h1 class="three four">Double Class</h1>
```

```css
.three.four { color: red; }
```

> #### Multiples

> We aren’t limited to only two here, we can combine as many classes and IDs into a single selector as we want.

```css
.snippet#header.code.red { color: red; }
```


重點：
- Multiple Class Selector 是用N個class selector 相接而成的selector，主要會選擇同時滿足N的class selector的DOM 節點
- ID and Class Selectors 是由多個class selector 和一個 id selector合併而成的selector來選擇同時滿足所有selector的DOM節點
- Multiple Class Selector 和 ID and Class Selectors 所採用的多個selector之間不會有任何符號，只會以.xxxxx來表示class selector 和#xxxxx來表示id selector


## 複習
#🧠 Multiple Class Selector 是什麼？ ->->-> `是用N個class selector 相接而成的selector，主要會選擇同時滿足N的class selector的DOM 節點`
<!--SR:!2022-09-14,10,250-->


#🧠 Multiple Class Selector 和 ID and Class Selectors 如何形成，用程式碼表示 ->->-> `.class1.class2 {} 和 #id.class1 { }`
<!--SR:!2022-09-14,10,250-->

#🧠 \#one.two { color: red; } 意味著什麼樣DOM節點才能被選擇到 ->->-> `id屬性為one且class屬於two的DOM 節點`
<!--SR:!2022-09-14,10,250-->

#🧠 .class1.class2 {...} 意味著什麼樣DOM節點才能被選擇到 ->->-> `class同時屬於class1和class2的DOM 節點`
<!--SR:!2022-09-14,10,250-->

---
Status: #🌱 
Tags:
[[CSS]]
Links:
References: