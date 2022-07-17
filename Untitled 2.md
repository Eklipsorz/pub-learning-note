

> To understand why you should use webpack, let's recap how we used JavaScript on the web before bundlers were a thing.

> There are two ways to run JavaScript in a browser. First, include a script for each functionality; this solution is hard to scale because loading too many scripts can cause a network bottleneck. The second option is to use a big `.js` file containing all your project code, but this leads to problems in scope, size, readability and maintainability.

重點：在還沒有使用webpack工具之前，要將瀏覽器執行JS，有兩個方式
- 第一點：替每一個業務邏輯寫一份獨立JS檔案並放在伺服器，然後分別由瀏覽器進行下載、解析、執行。
	- 衍生問題：這會因為檔案太多而使得網路傳輸成本增加，進而可能產生出 **要執行對應對應JS檔案時，但JS檔案還未下載好 ** 
- 第二點：將所有業務邏輯寫在同一份JS檔案並放在伺服器，然後讓瀏覽器下載、解析、執行
	- 衍生問題：由於業務邏輯全集中同一份檔案，而開發時也是同一份檔案，導致面臨開發時會遇到一系列有關於scope、易讀性、維護性、大小的問題，即為衍生出開發難度較高的檔案


> ## IIFEs - Immediately invoked function expressions
>
> IIFEs solve scoping issues for large projects; when script files are wrapped by an IIFE, you can safely concatenate or safely combine files without worrying about scope collision.
>
> The use of IIFEs led to tools like Make, Gulp, Grunt, Broccoli or Brunch. These tools are known as task runners, and they concatenate all your project files together.
>
> However, changing one file means you have to rebuild the whole thing. Concatenating makes it easier to reuse scripts across files but makes build optimizations more difficult. How can you find out if code is actually being used or not?
>
> Even if you only use a single function from lodash, you have to add the entire library and then squish it together. How do you treeshake the dependencies on your code? Lazy loading chunks of code can be hard to do at scale and requires a lot of manual work from the developer.

每一個JS業務邏輯皆以IIFE來表示，連接就以IIFE來連接


> ## Birth of JavaScript Modules happened thanks to Node.js[](https://webpack.js.org/concepts/why-webpack/#birth-of-javascript-modules-happened-thanks-to-nodejs)
> 
> Webpack runs on Node.js, a JavaScript runtime that can be used in computers and servers outside a browser environment.
> 
> When Node.js was released a new era started, and it came with new challenges. Now that JavaScript is not running in a browser, how are Node applications supposed to load new chunks of code? There are no html files and script tags that can be added to it.
> 
> CommonJS came out and introduced `require`, which allows you to load and use a module in the current file. This solved scope issues out of the box by importing each module as it was needed.

>  npm + Node.js + modules – mass distribution[](https://webpack.js.org/concepts/why-webpack/#npm--nodejs--modules--mass-distribution)


> JavaScript is taking over the world as a language, as a platform and as a way to rapidly develop and create fast applications.

But there is no browser support for CommonJS. There are no [live bindings](https://medium.com/webpack/the-state-of-javascript-modules-4636d1774358). There are problems with circular references. Synchronous module resolution and loading is slow. While CommonJS was a great solution for Node.js projects, browsers didn't support modules, so bundlers and tools like Browserify, RequireJS and SystemJS were created, allowing us to write CommonJS modules that run in a browser.

[[@webpackWhyWebpack]]


