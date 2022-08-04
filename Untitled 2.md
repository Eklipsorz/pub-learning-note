## 描述

[[@askieGuanYuWebpackTaShiShiMo]]

### What is module bundling?
> # What is module bundling?

> On a high level, module bundling is simply the process of stitching together a group of modules (and their dependencies) into a single file (or group of files) in the correct order.

> As with all aspects of web development, the devil is in the details. :)

重點：
- bundle：將多個事物捆綁成一個群組，bundling 是將多個事物捆綁成一個群組的行為
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


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@askieGuanYuWebpackTaShiShiMo]]