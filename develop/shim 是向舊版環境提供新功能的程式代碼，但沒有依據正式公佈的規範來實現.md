## 描述
[[@mdnShimMDNWeb]]
> A **shim** is a piece of code used to correct the behavior of code that already exists, usually by adding new API that works around the problem. This differs from a [polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill), which implements a new API that is not supported by the stock browser as shipped.

[[@ianPolyfillShiShiMo2022]]
> 而在polyfill之前，也有一個相類似的名詞 — shim，shim同樣也是為舊版環境提供現有功能的程式碼，但polyfill與shim最大的不同，是polyfill實現的功能都是官方正式公怖並實現的規範，shim則是實現原生沒有的功能（例如lowdash），而這也是 Remy Sharp 使用polyfill一詞去作具分的原因。

重點：
- shim 是一種程式代碼
- shim 向舊版環境提供新功能的程式代碼，但沒有依據正式公佈的規範來實現

## 複習
#🧠 Javascript : shim是什麼？  ->->-> `是一種程式代碼，向舊版環境提供新功能的程式代碼，但沒有依據正式公佈的規範來實現`
<!--SR:!2022-06-13,3,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[polyfill 是一個依據正式規範來實現瀏覽器未曾實現功能的程式代碼]]
References:
[[@ianPolyfillShiShiMo2022]]
[[@mdnShimMDNWeb]]