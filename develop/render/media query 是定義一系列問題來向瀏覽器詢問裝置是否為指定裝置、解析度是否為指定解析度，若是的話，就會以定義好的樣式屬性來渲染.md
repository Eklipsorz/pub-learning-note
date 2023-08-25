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
- media 對於網頁而言，會是指能夠讓使用者接收網頁畫面並呈現的裝置
- media query 中的 media會源自於傳播媒體的media。
- media query 則是開發者定義一系列問題來向瀏覽器詢問裝置是否為指定裝置、解析度是否為指定解析度，若是的話，就會以定義好的樣式屬性來渲染
- media query 是由 @media作為開頭 、向瀏覽器發問的問題、對於符合問題情景的樣式屬性
```
@media query {
	property1: value1;
	.
	.
	.
}
```
- media query 若滿足的話，裡頭的樣式屬性會如何加入至CSSOM? 利用CSS specificity 來決定CSSOM的最終內容
- 常見的為解析度：
	- @media (max-width: xxxx px)：指定在xxxx px以下就利用CSS specificity 來決定CSSOM的最終內容。
	- @media (min-width: xxxx px)：指定在xxxx px以上就利用CSS specificity 來決定CSSOM的最終內容。
### media query的media 命名緣由

> the main ways that large numbers of people receive information and entertainment, that is television, radio, newspapers and the internet

重點：
- 在傳播媒體上，media 是接收資訊並呈現其資訊的裝置


[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
## 複習

#🧠 media query的media 命名緣由為何？ ->->-> `在傳播媒體上，media 是接收資訊並呈現其資訊的裝置`
<!--SR:!2023-08-25,196,250-->


#🧠 在傳播媒體上，media 原意為讓人們接收資訊的裝置或者介質，若以網頁來說的話，會是什麼？->->-> `對於網頁而言，會是指能夠讓使用者接收網頁畫面並呈現的裝置`
<!--SR:!2025-01-25,518,250-->

#🧠 media query 是什麼？ ->->-> `開發者定義一系列問題來向瀏覽器詢問裝置是否為指定裝置、解析度是否為指定解析度，若是的話，就會以定義好的樣式屬性來渲染`
<!--SR:!2025-03-04,561,250-->

#🧠 media query 形式大概是什麼？ ->->-> `@media query { properties }`
<!--SR:!2023-10-31,66,210-->

#🧠 media query 中的 @media (max-width: xxxx px) 是做什麼？ ->->-> `指定在xxxx px以下就利用CSS specificity 來決定CSSOM的最終內容。`
<!--SR:!2024-02-15,323,250-->

#🧠 media query 若滿足的話，裡頭的樣式屬性會如何加入至CSSOM？ ->->-> `利用CSS specificity 來決定CSSOM的最終內容`
<!--SR:!2025-02-08,539,250-->

#🧠 media query 中的 @media (min-width: xxxx px) 是做什麼？ ->->-> `指定在xxxx px以上就利用CSS specificity 來決定CSSOM的最終內容。`
<!--SR:!2024-07-22,334,230-->



---
Status: #🌱 
Tags:
[[CSS]]
Links:
[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
References:
[[@mdnUsingMediaQueries]]
[[@wikidataMediaQueries2021]]