## 描述









 webpack之前，前端網頁得為了權衡開發者是否容易開發而搞模組化和瀏覽器執行效能這兩個目標，但後來發現不論走哪一個方向，另一個總是無法達成，因此那個時期沒辦法以模組化的形式來寫前端，為了解決這樣困境，有人就想出**開發時就以易於人類開發的結構來開發，而實際部署時就以易於瀏覽器執行的形式來呈現**這個目標，具體的話，就是找一個類似編譯器的程式來充當開發和部署之間的橋樑 (已编辑)

編譯器就為webpack


webpack是一種工具，專門將多個模組(包含圖片等靜態檔案)綑綁成由一個單一檔案或者一組檔案所構成的整合物(bundle)，在這裏的捆綁會是以特定某種轉換手段，而整合物則是由轉換手段轉換過來的產物。

在這裏多個模組會是前端框架、CSS/CSS預處理器

在這裏整合物會適應於瀏覽器的執行，但對於人類的開發上




webpack

多個js -> 統整成一個js
圖片 -> 壓縮
css -> 遇到preprocessor就執行css，然後將css


### What is module bundling?
[[@askieGuanYuWebpackTaShiShiMo]]
> # What is module bundling?

> On a high level, module bundling is simply the process of stitching together a group of modules (and their dependencies) into a single file (or group of files) in the correct order.

> As with all aspects of web development, the devil is in the details. :)

重點：
- bundle：將多個事物捆綁成一個群組，bundling 是將多個事物捆綁成一個群組的行為，若加以延伸的話，可以將多個事物透過某種轉換手段來當作綑綁，並轉換成整合物
> to gather or tie in a bundle(一捆)
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
[[Rendering]]
Links:
References:
[[@wikidataJiJianHua2022]]
[[@askieGuanYuWebpackTaShiShiMo]]