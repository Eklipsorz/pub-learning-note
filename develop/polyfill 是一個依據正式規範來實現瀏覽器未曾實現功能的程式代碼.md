
## 描述
[[@PolyfillMDNWeb]]
> A polyfill is a piece of code (usually JavaScript on the Web) used to provide modern functionality on older browsers that do not natively support it.

[[@ianPolyfillShiShiMo2022]]

> 而在polyfill之前，也有一個相類似的名詞 — shim，shim同樣也是為舊版環境提供現有功能的程式碼，但polyfill與shim最大的不同，是polyfill實現的功能都是官方正式公怖並實現的規範，shim則是實現原生沒有的功能（例如lowdash），而這也是 Remy Sharp 使用polyfill一詞去作具分的原因。

重點：
- polyfill 是一個程式代碼
- polyfill 主要依據官方正式公佈實現的規範而實現的功能，而這串代碼對於瀏覽器而言，瀏覽器沒去實現該對應功能
- 也就是實現瀏覽未曾實現功能，但這功能是出自於官方規範中



### polyfill 命名緣由

[[@sharpWhatPolyfill2010]]
由 Remy Sharp 發明的名詞和概念
> Polyfill just kind of came to me, but it fitted my requirements. Poly meaning it could be solved using any number of techniques - it wasn't limited to just being done using JavaScript, and fill would fill the hole in the browser where the technology needed to be. It also didn't imply "old browser" (because we need to polyfill new browser too).

poly-
> many

重點：
- poly- 代表數量層面下表示多的意思
- polyfill 中的 poly 表示使用任意數量的技術解決，fill則是表示填補宿主環境或者瀏覽器下所擁有的漏洞，合併再一起就是使用任意數量之技術，而這些技術會專注解決宿主環境或者瀏覽器下所擁有的漏洞


## 複習
#🧠 Javascript： polyfill是什麼樣的東西(提示：代碼) ->->-> `polyfill 是一個程式代碼，polyfill 主要依據官方正式公佈實現的規範而實現的功能，而這串代碼對於瀏覽器而言，瀏覽器沒去實現該對應功能，也就是實現瀏覽未曾實現功能，但這功能是出自於官方規範中`
<!--SR:!2024-04-12,405,250-->

#🧠 poly- 表示什麼意思？ ->->-> `代表數量層面下表示多的意思`
<!--SR:!2023-12-20,173,250-->

#🧠 polyfill 在程式開發下的命名緣由為何 ->->-> `poly 表示使用任意數量的技術解決，fill則是表示填補宿主環境或者瀏覽器下所擁有的漏洞，合併再一起就是使用任意數量之技術，而這些技術會專注解決宿主環境或者瀏覽器下所擁有的漏洞`
<!--SR:!2023-06-19,67,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[shim 是一種小型函式庫，擺放在程式模組A和程式模組B的呼叫關係之間並進行攔截和修改，並讓他們都能合法呼叫和獲取]]
References:
[[@PolyfillMDNWeb]]
[[@sharpWhatPolyfill2010]]
[[@ianPolyfillShiShiMo2022]]