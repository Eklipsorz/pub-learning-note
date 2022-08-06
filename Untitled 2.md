## 描述

### 新技術載入的問題
[[@ithomeXunMiWebpack03]] 所描述的新技術載入的問題：
> 網頁技術在現代急遽變化，遇到了各種問題，也出現了許多的解決方案，以下做個總覽：

```
-   JavaScript
    -   宿主環境對各語法支援度不一：Babel
    -   是弱型別語言：TypeScript, flow
-   CSS
    -   宿主環境對各語法支援度不一：PostCSS
    -   語法過於簡單：SASS
    -   是靜態的：CSS in JS
-   HTML
    -   是靜態的：Pug, Template Syntax
```


> 雖然前端工程因為語言的限制產生了許多的問題，但是也都有了對應的方案可以解決，但這些方案都有一個共通的問題，那就是**需要配置相對應的轉譯器才能在瀏覽器上執行**
> 
> 原本這些解決方案的目的是要加速開發的，但每次要執行時都要手動啟動編譯器，反而會降低開發速度，這時候還好有像是 Webpack 這類 bundler 工具的出現，才能順利地將這些工具帶入開發鍊中。


#### JavaScript 技術演進
```
-   JavaScript
    -   宿主環境對各語法支援度不一：Babel
    -   是弱型別語言：TypeScript, flow
```

JavaScript


> Babel is a free and open-source JavaScript transcompiler that is mainly used to convert ECMAScript 2015+ (ES6+) code into a backwards compatible version of JavaScript that can be run by older JavaScript engines.



#### CSS 技術演進
```
-   CSS
    -   宿主環境對各語法支援度不一：PostCSS
    -   語法過於簡單：SASS
    -   是靜態的：CSS in JS
```

#### HTML 技術演進
```
-   HTML
    -   是靜態的：Pug, Template Syntax
```




重點：
- 新技術載入的問題都源自於**為了加速開發和解決問題，而提供特定語言體系和編譯器來轉換成能夠讓瀏覽器識別得出來的HTML、JS、CSS**：從特定語言體系的角度來解決問題和開發問題，而非以HTML、JS、CSS本身內容
- 這類型的技術開發時都需要手動啟動編譯才能讓他們從特定語言體系轉換成HTML、JS、CSS，數量越多，就難以管理編譯上的執行




## 複習
Status: #🌱 
Tags:
[[JavaScript]] - [[webpack]]
Links:
[[transcompiler 是一種compiler ，只是強調著這類型的compiler會是將高階程式語言轉換成另一個高階程式語言]]
[[strong type 和 weak type 的 強弱是相對的，沒有絕對的定義，需要拿其他語言特性來比較目前語言特性才有強弱之分，越強就代表資料型別越明確，越弱就代表資料型別越不明確]]
References:
[[@ithomeXunMiWebpack03]]