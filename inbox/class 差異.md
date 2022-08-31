




## 描述


[[@pjchenderJiShuFenXiangCSSZhongDeDuoChongXuanZeQiMultiple]]
> ### CSS 部分

> 那麼為什麼我們有時候會看到.one .two{ }這樣子的寫法呢？  
  
> 這裡，我們需要進一步區別到底是.one.two{ }，.one .two{ }，或這是.one, .two{ }。乍看之下，這三者都長得很像，但實際上是有很大的不同的。  
  

> -   第一個的 one 和 two 中間沒有包含空格，這個的意思表示，某個區塊必須同時具有 one 和 two 的 class 時，才能被 CSS 所選擇到到。
> -   第二個的 one 和 two 中間包含空格，意思是指，我必須要是在 one 裡面的 two，才會被選擇到。
> -   第三個的 one 和 two 中間包含逗號，意思是指 class 中有 one 或 two，都會被編輯器所選擇到。

>   簡單來說，沒空格表示必須同時包含才會被選取；有空格表示後面的 class 被鑲嵌在前面的 class 中才會被選取；逗號則表示只要有其中一個 class 就會被選取到 。




### 
[[@chriscoyierMultipleClassID2010]]

> Can you spot the difference between these two selectors?

```css
#header.callout {  }
#header .callout { }
```

> They look nearly identical, but the top one has no space between `#header` and `.callout` while the bottom one does. This small difference makes a huge difference in what it does. To some of you, that top selector may seem like a mistake, but it’s actually a quite useful selector. Let’s see the difference, what that top selector means, and exploring more of that style selector.

> Here is the “plain English” of `#header .callout`:

> Select all elements with the class name _callout_ that are decendents of the element with an ID of _header_.

>Here is the “plain English” of `#header.callout`:

> Select the element which has an ID of _header_ and also a class name of _callout_.
>
> Maybe this graphic will make that more clear:

![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2021/04/classplusid.png?resize=570%2C190&ssl=1)


### 




## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[CSS]]
Links:
References:
[[@pjchenderJiShuFenXiangCSSZhongDeDuoChongXuanZeQiMultiple]]
[[@chriscoyierMultipleClassID2010]]