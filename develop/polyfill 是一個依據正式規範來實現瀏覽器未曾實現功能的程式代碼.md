
## 描述
[[@PolyfillMDNWeb]]
> A polyfill is a piece of code (usually JavaScript on the Web) used to provide modern functionality on older browsers that do not natively support it.

[[@ianPolyfillShiShiMo2022]]

> 而在polyfill之前，也有一個相類似的名詞 — shim，shim同樣也是為舊版環境提供現有功能的程式碼，但polyfill與shim最大的不同，是polyfill實現的功能都是官方正式公怖並實現的規範，shim則是實現原生沒有的功能（例如lowdash），而這也是 Remy Sharp 使用polyfill一詞去作具分的原因。

重點：
- polyfill 是一個程式代碼
- polyfill 主要依據官方正式公佈實現的規範而實現的功能，而這串代碼對於瀏覽器而言，瀏覽器沒去實現該對應功能
- 也就是實現瀏覽未曾實現功能，但這功能是出自於官方規範中

### 與shim比較
1. 共同點：polyfill 和 shim 兩者皆向執行環境或者對應環境提供環境所沒有的功能之實現代碼
2. 不同點：polyfill是依據正式規範來實現，shim則不一定依據正式規範來實現

## 複習
#🧠 Javascript： polyfill是什麼樣的東西(提示：代碼) ->->-> `polyfill 是一個程式代碼，polyfill 主要依據官方正式公佈實現的規範而實現的功能，而這串代碼對於瀏覽器而言，瀏覽器沒去實現該對應功能，也就是實現瀏覽未曾實現功能，但這功能是出自於官方規範中`
<!--SR:!2022-09-21,65,250-->

#🧠 Javascript： polyfill 和 shim 有什麼共同點？ ->->-> `polyfill 和 shim 兩者皆向執行環境或者對應環境提供環境所沒有的功能之實現代碼`
<!--SR:!2022-10-02,68,230-->

#🧠 Javascript： polyfill 和 shim 有什麼不同點？ ->->-> `polyfill是依據正式規範來實現，shim則不一定依據正式規範來實現`
<!--SR:!2022-08-03,32,230-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[shim 是向舊版環境提供新功能的程式代碼，但沒有依據正式公佈的規範來實現]]
References:
[[@PolyfillMDNWeb]]
[[@ianPolyfillShiShiMo2022]]