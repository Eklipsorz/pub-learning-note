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


重點：
- webpack 是一個網頁應用程式的模組打包器(bundler)
- webpack 主要用途會是將開發階段的多個模組分別按照模組種類來進行轉換打包所需的基本元件，然後再將基本元件包在一塊以構成單個bundle或者數個bundle
- webpack的產物會是模組或者稱之為bundle，可供人以模組形式來加載其內容
- bundle 內容通常會是 js、css、image、html (若有template language的話)

既然是模組，那必定有使用模組的一方


webpack

多個js -> 統整成一個js
圖片 -> 壓縮
css -> 遇到preprocessor就執行css，然後將css

### bundle 命名緣由
bundle
> verb - to gather or tie in a bundle(一捆)
> noun - a number of things that have been fastened or are held together

重點：
- bundle：動詞是將多個事物捆綁成一個群組；名詞是指一系列被捆棒在一起的產物。
- bundling 是將多個事物捆綁成一個群組的行為
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