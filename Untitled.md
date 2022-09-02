## 描述

[[@wikidataMediaQueries2021]]
> Media queries is a feature of CSS 3 allowing content rendering to adapt to different conditions such as screen resolution

[[@mdnUsingMediaQueries]]
> Media queries are useful when you want to modify your site or app depending on a device's general type (such as print vs. screen) or specific characteristics and parameters (such as screen resolution or browser viewport width).



> A media query is composed of an optional media type and any number of media feature expressions, which may optionally be combined in various ways using logical operators. Media queries are case-insensitive.


>  Many media features are range features, which means they can be prefixed with "min-" or "max-" to express "minimum condition" or "maximum condition" constraints. For example, this CSS will apply styles only if your browser's viewport width is equal to or narrower than 12450px:


```
// xxxx px 以下 就採用
@media (max-width: xxxx px) { /* … */ }

// xxxx px 以上 就採用
@media (min-width: xxxx px) { /* … *}
```

重點：
- 是瀏覽器對於目前media


## 複習


---
Status: #🌱 #📓 
Tags:
[[CSS]]
Links:
References:
[[@mdnUsingMediaQueries]]
[[@wikidataMediaQueries2021]]