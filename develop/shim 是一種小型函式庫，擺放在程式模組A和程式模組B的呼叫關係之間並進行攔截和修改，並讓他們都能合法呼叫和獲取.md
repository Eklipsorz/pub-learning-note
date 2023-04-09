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
- 主要是在特定模組A和B之間的呼叫關係間來攔截並轉換相互都能接收的形式，來讓A和B不因為版本、語法而受限其呼叫關係：
	- 本身提供一個呼叫介面，並於特定程式模組A和特定程式模組B之間的呼叫關係進行A對於B單方面的呼叫攔截，攔截過程中會將A的參數和A本身導入至介面，並根據B的現有版本狀況來修改和編輯參數來導入至另一種函式呼叫形式來呼叫B
	- 由B將結果導入至Shim，並且為了A能夠容易接收其結果形式，會將結果轉換並給A
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677921968/blog/programming/shim/shim-example_fjauto.png)
- shim所需要做的轉換具體有：
	- A 單方面對於B的呼叫形式，理由為確保A能夠合法呼叫它所想要的資源
	- B 原定回傳給A的結果，理由為確保A接收到它能接受的形式
- 應用：
	- 允許老舊模組能夠在新系統環境下繼續使用：將老舊模組視為模組A以及將新系統環境視為模組B，並且在他們添加shim介面來攔截和修改
	- 允許新模組能夠在老舊系統環境下繼續使用：將新模組視為模組A以及將老舊系統環境視為模組B，並且在他們添加shim介面來攔截和修改

### shim 命名緣由

> a small object or piece of material used between two parts of something to make them fit together, or to prevent them rubbing against each other

重點：
- shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦






## 複習

#🧠 shim 命名緣由為何？ ->->-> `shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦`
<!--SR:!2023-05-09,40,250-->

#🧠 shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦，那麼在程式語言下的shim會是？->->-> `shim 是一種小型函式庫`
<!--SR:!2023-05-13,43,250-->

#🧠 shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦，那麼在程式語言下的shim會是一種小型函式庫，用途為何？ ->->-> `主要是在特定模組A和B之間的呼叫關係間來攔截並轉換相互都能接收的形式，來讓A和B不因為版本、語法而受限其呼叫關係`
<!--SR:!2023-04-19,11,230-->

#🧠 shim 主要用途為主要是在特定模組A和B之間的呼叫關係間來攔截並轉換相互都能接收的形式，來讓A和B不因為版本、語法而受限其呼叫關係，具體是如何實現 ->->-> `	- 本身提供一個呼叫介面，並於特定程式模組A和特定程式模組B之間的呼叫關係進行A對於B單方面的呼叫攔截，攔截過程中會將A的參數和A本身導入至介面，並根據B的現有版本狀況來修改和編輯參數來導入至另一種函式呼叫形式來呼叫B - 由B將結果導入至Shim，並且為了A能夠容易接收其結果形式，會將結果轉換並給A`
<!--SR:!2023-05-11,41,250-->




#🧠 在程式語言下的shim會是一種小型函式庫，主要會在模組A和模組B的呼叫關係進行轉換，請問shim所需要的轉換會是如何？理由又會是如何？ ->->-> `	- A 單方面對於B的呼叫形式，理由為確保A能夠合法呼叫它所想要的資源 - B 原定回傳給A的結果，理由為確保A接收到它能接受的形式`
<!--SR:!2023-05-30,52,250-->

#🧠 shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦，那麼在程式語言下的shim會是一種小型函式庫，用途為何？畫圖來說明 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677921968/blog/programming/shim/shim-example_fjauto.png)`
<!--SR:!2023-06-07,61,250-->

#🧠 shim 會是一個實體物件，主要放在多個特定事物之間的縫隙，使這些東西能因為實體物件而相連或者阻止摩擦，那麼在程式語言下的shim會是一種小型函式庫，用途為![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677921968/blog/programming/shim/shim-example_fjauto.png)，請解釋以下作用 ->->-> ``
<!--SR:!2023-06-06,58,250-->

#🧠 在程式語言下的shim會是一種小型函式庫，主要會在模組A和模組B的呼叫關係進行轉換，其應用會是如何？為何可以這樣做->->-> `	- 允許老舊模組能夠在新系統環境下繼續使用：將老舊模組視為模組A以及將新系統環境視為模組B，並且在他們添加shim介面來攔截和修改 - 允許新模組能夠在老舊系統環境下繼續使用：將新模組視為模組A以及將老舊系統環境視為模組B，並且在他們添加shim介面來攔截和修改`
<!--SR:!2023-04-09,24,250-->





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