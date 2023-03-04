## 描述
[[@mdnShimMDNWeb]]
> A **shim** is a piece of code used to correct the behavior of code that already exists, usually by adding new API that works around the problem. This differs from a [polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill), which implements a new API that is not supported by the stock browser as shipped.

[[@ianPolyfillShiShiMo2022]]
> ~~而在polyfill之前，也有一個相類似的名詞 — shim，shim同樣也是為舊版環境提供現有功能的程式碼，但polyfill與shim最大的不同，是polyfill實現的功能都是官方正式公怖並實現的規範，shim則是實現原生沒有的功能（例如lowdash），而這也是 Remy Sharp 使用polyfill一詞去作具分的原因。~~

[[@ShimComputing2023]]
> In computer programming, a shim is a library that transparently intercepts API calls and changes the arguments passed, handles the operation itself or redirects the operation elsewhere.


[[@DianPianChengShiSheJiWeiJiBaiKe]]
> 在程式設計領域，墊片（英語：shim）是一種小型函式庫，可以用來截取 API 呼叫、修改傳入參數，最後自行處理對應操作或者將操作交由其它地方執行。
> 墊片可以在新環境中支援老 API，也可以在老環境裡支援新 API。一些程式並沒有針對某些平台開發，也可以通過使用墊片來輔助執行。



重點：
- shim 是一種小型函式庫，主要用途為：
	- 本身提供一個呼叫介面，並於特定程式模組A和特定程式模組B之間的呼叫關係進行A對於B單方面的呼叫攔截，攔截過程中會將A的參數和A本身導入至介面，並根據B的現有版本狀況來修改和編輯參數來試圖調用B的所擁有資源給A
- 應用為：
	- 

### shim 命名緣由

> a small object or piece of material used between two parts of something to make them fit together, or to prevent them rubbing against each other

重點：
- shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦






## 複習
#🧠 Javascript : shim是什麼？  ->->-> `是一種程式代碼，向舊版環境提供新功能的程式代碼，但不一定依據正式公佈的規範來實現`
<!--SR:!2023-04-13,192,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[polyfill 是一個依據正式規範來實現瀏覽器未曾實現功能的程式代碼]]
References:
[[@ianPolyfillShiShiMo2022]]
[[@mdnShimMDNWeb]]
[[@ShimComputing2023]]
[[@DianPianChengShiSheJiWeiJiBaiKe]]