## 描述


### 提出原因
[[webpack 技術提出原因為解決JavaScript 的模組化問題和新技術載入的問題]]


### webpack 是什麼？

## 基本介紹
[[@ithomeXunMiWebpack04]] 描述
> webpack 是 **JavaScript 應用程式的模組打包器**。
> 它將各模組間的相依關係繪製成[相依圖](https://webpack.js.org/concepts/dependency-graph/)(dependency graph)，依照相依圖解析並處理每一個模組，最後建置成一個或多個 bundle 。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659807833/blog/webpack/webpack-js-bundle_jn830n.png)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659807833/blog/webpack/webpack-image-bundle_gjk6o7.png)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659807833/blog/webpack/webpack-asset-bundle_ewuwit.png)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659807834/blog/webpack/webpack-css-bundle_w4jx7s.png)

![](https://ics.media/entry/12140/images/160519_webpack_is__960.png)

重點：
- webpack 主要是一個JavaScript應用程式的模組打包器(bundler)
- webpack 具體會是將開發階段的多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，然後再將基本元件包在一塊以構成單個bundle或者數個bundle
- webpack的產物會是模組或者稱之為bundle.js，可供其他程式以模組形式來加載其內容
- 在進行打包時會所會做的轉換會是：
	- JS種類模組：支援JS模組化的所有方法並從中統一成同一個模組實現的模組、轉譯(transcompile)、優化程式碼
	- CSS種類模組：將以CSS preprocessor 語法構成的程式碼編譯成CSS、幫忙後製CSS、優化
	- HTML種類模組(包含template  language)：優化、自動加載
	- 圖片模組：將圖片壓縮
- 使用模組的那一方會是HTML、template language構成的template
> 既然是模組，那必定有使用模組的一方



### webpack entry 
> 開發者要跟 webpack 說明哪個模組是**建置相依圖時的起點**，因此需要配置 `entry` 屬性。
> 啟動 webpack 時，會先解析起始模組，找出起始模組是否有相依其他的模組，接著再往下一個模組搜尋，一直到找不到相依模組時，如此一來就形成了相依圖。
> 
> `entry` 的預設值為 `./src/index.js`

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659811692/blog/webpack/webpack-entry_cemvwe.png)


重點：
- entry 是指從哪個檔案為中心來進行模組依賴關係，
- entry 具體用並將他所經過的檔案都做轉換(優化)
- entry 通常為javascript檔案

### bundle 命名緣由
bundle
> verb - to gather or tie in a bundle(一捆)
> noun - a number of things that have been fastened or are held together

重點：
- bundle：動詞是將多個事物捆綁成一個群組；名詞是指一系列被捆棒在一起的產物。
- bundling ：是將多個事物捆綁成一個群組的行為、過程
- bundler：進行綑綁行為的一方
### What is module bundling?
[[@askieGuanYuWebpackTaShiShiMo]]
> # What is module bundling?

> On a high level, module bundling is simply the process of stitching together a group of modules (and their dependencies) into a single file (or group of files) in the correct order.

> As with all aspects of web development, the devil is in the details. :)

重點：
- module bundling 是會指將一組模組以特定順序來拼接成一個單一檔案或者一組檔案


### Why bundle modules at all?

> # Why bundle modules at all?

> When you divide your program into modules, you typically organize those modules into different files and folders. Chances are, you’ll also have a group of modules for the libraries you’re using, like Underscore or React.

> As a result, each of those files has to be included in your main HTML file in a **_\<script\>_** tag, which is then loaded by the browser when a user visits your home page. Having separate **_\<script\>_** tags for each file means that the browser has to load each file individually: one… by… one.

> …Which is bad news for page load time.

> To get around this problem, we bundle, or “concatenate” all our files into one big file (or a couple files as the case may be) in order to reduce the number of requests. When you hear developers talking about the “build step” or “build process,” this is what they’re talking about.

> Another common approach to speed up the bundling operation is to “minify” the bundled code. Minification is the process of removing unnecessary characters from source code (e.g. whitespace, comments, new line characters, etc.), in order to reduce the overall size of the content without changing the functionality of the code.

> Less data means less browser processing time, which in turn reduces the time it takes to download files. If you’ve ever seen a file that had a “min” extension like “[underscore-min.js](https://github.com/jashkenas/underscore/blob/master/underscore-min.js)”, you probably noticed that the minified version is pretty tiny (and unreadable) compared to the [full version](https://github.com/jashkenas/underscore/blob/master/underscore.js).

> Task runners like Gulp and Grunt make concatenation and minification straightforward for developers, ensuring that human-readable code stays exposed for developers while machine-optimized code gets bundled for browsers.

重點：
- 利用module bundling
- 極簡化 minify：是一種移除

#### minify 是什麼技術
[[@wikidataJiJianHua2022]] 描述的minify：

> 在程式語言 (尤其是 JavaScript) 的範疇裡，指的是在不影響功能的情況下，移除所有非功能性必要之原始碼字元（如：空白、換行、註解、以及些許的區塊辦識子）

[[@askieGuanYuWebpackTaShiShiMo]] 描述的好處：
> Less data means less browser processing time, which in turn reduces the time it takes to download files

重點：
- minify 是指在程式語言中，在不影響功能下，從原始碼移除所有不會影響功能的字元，比如空白、換行、註解
- minify 好處是簡化的資料會較少，這會使得瀏覽器花較少的時間去下載和處理
- minify 壞處是易讀性很差

## 複習
#🧠  webpack 是什麼？ ->->-> `主要是一個JavaScript應用程式的模組打包器(bundler)`
<!--SR:!2022-08-19,9,250-->
#🧠 bundle 命名緣由，動詞和名詞分別為什麼？->->-> `bundle：動詞是將多個事物捆綁成一個群組；名詞是指一系列被捆棒在一起的產物。`
<!--SR:!2022-08-18,8,250-->

#🧠 minify 是什麼樣的技術？ ->->-> `是指在程式語言中，在不影響功能下，從原始碼移除所有不會影響功能的字元，比如空白、換行、註解`
<!--SR:!2022-08-20,9,250-->

#🧠 minify 會移除什麼字元，比如說？ ->->-> `空白、換行、註解`
<!--SR:!2022-08-21,10,250-->

#🧠 minify 優缺點？ ->->-> `minify 好處是簡化的資料會較少，這會使得瀏覽器花較少的時間去下載和處理 - minify 壞處是易讀性很差`
<!--SR:!2022-08-18,7,250-->

#🧠 bundling 命名緣由是什麼？ ->->-> `是將多個事物捆綁成一個群組的行為、過程`
<!--SR:!2022-09-02,17,250-->

#🧠 bundler 命名緣由是什麼？ ->->-> `進行綑綁行為的一方`
<!--SR:!2022-08-20,10,250-->

#🧠 webpack 是什麼？具體是什麼？ ->->-> `主要是一個JavaScript應用程式的模組打包器(bundler)，具體會是將開發階段的多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，然後再將基本元件包在一塊以構成單個bundle或者數個bundle`
<!--SR:!2022-08-19,9,250-->

#🧠 webpack 的產物會是什麼？ ->->-> `模組或者稱之為bundle.js`
<!--SR:!2022-08-20,10,250-->

#🧠 webpack 的產物能做什麼？ ->->-> `可供其他程式以模組形式來加載其內容`
<!--SR:!2022-08-19,9,250-->

#🧠 webpack 會將多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，那麼具體轉換是什麼 ->->-> `JS種類模組：支援JS模組化的所有方法並從中統一成同一個模組實現的模組、轉譯(transcompile)、優化程式碼。CSS種類模組：將以CSS preprocessor 語法構成的程式碼編譯成CSS、幫忙後製CSS、優化。HTML種類模組(包含template  language)：優化、自動加載。圖片模組：將圖片壓縮`
<!--SR:!2022-08-19,9,250-->



#🧠 webpack 會將多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，那麼對於JS種類模組的具體轉換是什麼 ->->-> `JS種類模組：支援JS模組化的所有方法並從中統一成同一個模組實現的模組、轉譯(transcompile)、優化程式碼`
<!--SR:!2022-08-17,7,250-->


#🧠 webpack 會將多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，那麼對於CSS種類模組的具體轉換是什麼 ->->-> `將以CSS preprocessor 語法構成的程式碼編譯成CSS、幫忙後製CSS、優化`
<!--SR:!2022-09-02,17,250-->


#🧠 webpack 會將多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，那麼對於HTML種類模組的具體轉換是什麼->->-> `優化、自動加載`
<!--SR:!2022-08-17,7,250-->

#🧠 webpack 會將多個與JS相關的模組(圖片、CSS、JS)分別按照模組種類來進行轉換以建立打包所需的基本元件，那麼對於圖片種類模組的具體轉換是什麼 ->->-> `將圖片壓縮`
<!--SR:!2022-08-21,10,250-->

#🧠 webpack 最後產生出的模組數就會是1個嗎？ ->->-> `不一定，具體還要看開發者指定`
<!--SR:!2022-08-21,10,250-->

#🧠 webpack 的產物會由誰來加載？ ->->-> `使用模組的那一方會是HTML、template language構成的template`
<!--SR:!2022-08-17,7,250-->

#🧠 webpack 會處理template language所構成的template嗎？ 如何處理->->-> `會，只要和entry扯上關係就會處理，具體會是優化、自動加載`
<!--SR:!2022-08-19,9,250-->


#🧠 webpack entry 是什麼？會做什麼->->-> `entry 是指從哪個檔案為中心來進行模組依賴關係，並將他所經過的檔案都做轉換(優化)`
<!--SR:!2022-09-02,17,250-->

#🧠 webpack entry 是什麼檔案？->->-> `javascript檔案`
<!--SR:!2022-08-20,10,250-->

---
Status: #🌱 
Tags:
[[Rendering]] - [[JavaScript]] - [[webpack]]
Links:
[[webpack 技術提出原因為解決JavaScript 的模組化問題和新技術載入的問題]]
[[HTML、CSS、JS隨著時代更迭而演進成需要事前轉譯來解決各自問題、根據情況來產生對應的CSS、HTML]]
References:
[[@ithomeXunMiWebpack04]]
[[@wikidataJiJianHua2022]]
[[@askieGuanYuWebpackTaShiShiMo]]