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
- media 對於網頁而言，會是指能夠顯示網頁畫面的畫面
- media query 則是定義一系列問題來向瀏覽器詢問裝置是否為指定裝置、解析度是否為指定解析度，若是的話，就會以定義好的樣式屬性來渲染
- media query 是由 @media作為開頭 、向瀏覽器發問的問題、對於符合問題情景的樣式屬性
```
@media query {
	property1: value1;
	.
	.
	.
}
```

- 常見的為解析度：
	- @media (max-width: xxxx px)：指定在xxxx px以下就採用
	- @media (min-width: xxxx px)：指定在xxxx px以上就採用
### media 命名緣由

> the main ways that large numbers of people receive information and entertainment, that is television, radio, newspapers and the internet

重點：
- media 為讓人們接收資訊的裝置或者介質

## 複習


---
Status: #🌱 #📓 
Tags:
[[CSS]]
Links:
References:
[[@mdnUsingMediaQueries]]
[[@wikidataMediaQueries2021]]