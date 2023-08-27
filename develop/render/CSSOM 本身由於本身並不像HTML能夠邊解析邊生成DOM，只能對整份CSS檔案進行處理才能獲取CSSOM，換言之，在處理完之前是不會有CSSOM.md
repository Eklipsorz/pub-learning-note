## 描述

### CSS 不會阻塞 DOM Tree的建立，但會阻塞頁面的顯示
> # css 阻塞了什么

> 当我们解析 HTML 时遇到 link 标签或者 style 标签时，就会计算样式，构建CSSOM。
>
> css不会阻塞dom树的构建，但是会阻塞页面的显示。我们依然用一个例子来测试：

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" type="text/css" href="https://h5.sinaimg.cn/m/weibo-pro/css/chunk-vendors.d6cac585.css">
</head>
<body>
  <div class="woo-spinner-filled">hello world</div>
  <div>hello world2</div>
</body>
</html>
```
![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1930c65c9f2249ca9b8a4e7e1854a84a~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)



> 使用一个外部css文件，打开`Slow 3G`模拟比较慢的网速，可以看到，DOMContentLoaded事件触发只用了30ms，页面此时依然是空白，而几乎是loaded事件2.92s发生时，页面才出现内容。

> 原因是，**浏览器在构建 CSSOM 的过程中，不会渲染任何已处理的内容。即便 DOM 已经解析完毕了，只要 CSSOM 不没构建好，页面也不会显示内容。**


重點：
- 當瀏覽器的HTML 解析器解析HTML內容，若發現 link標籤或者style標籤時，如果是指定CSS檔案，就會生成非同步任務A去負責載入CSS檔案、解析其內容轉成CSSOM。
-  CSSOM的構建任務 本身不會阻塞DOM的建立，但會阻塞瀏覽器後續的渲染內容任務
- 原本從HTML解析成DOM之後，就會搭配CSSOM來打造Rendering Tree，接著執行渲染內容的任務(layout & paint)：
	- 若HTML解析成DOM完成之後，CSSOM還未建立完成，就會阻塞打造Rendering Tree以及後續的渲染任務，直到CSSOM建立完成
	- 若HTML解析成DOM完成之後，CSSOM也跟著建立完成，就會順勢執行渲染任務。
- 由於CSS本身在還沒處理完之前是不會有CSSOM，為了確保Rendering能夠使用到CSSOM，會讓CSSOM建構任務阻塞JS。


#### 閃爍
> **只有当我们遇到 link 标签或者 style 标签时，才会构建CSSOM**，所以如果 link 标签之前有dom元素，当加载css发生阻塞时，浏览器会将前面已经构建好的DOM元素渲染到屏幕上，以减少白屏的时间。比如下面这样：

```
<body>
  <div class="woo-spinner-filled">hello world</div>
  <link rel="stylesheet" type="text/css" href="https://h5.sinaimg.cn/m/weibo-pro/css/chunk-vendors.d6cac585.css">
  <div>hello world2</div>
</body>
```


> 这样做会导致一个问题，就是页面闪烁，在css被加载之前，浏览器按照默认样式渲染 `<div class="woo-spinner-filled">hello world</div>`，当css加载完成，会为该div计算新的样式，重新渲染，出现闪烁的效果。
>
> 为了避免页面闪烁，通常 link 标签都放在head中。

重點：

- 若遇到link標籤或者style標籤之前就有DOM，那麼瀏覽器會在那之前執行該DOM結構上的渲染
- 若接著讀取DOM之後的link標籤或者style標籤的話，就會觸發CSSOM的建立任務，而當完成之後，會重新刷新DOM之前的畫面，這時會有閃爍的效果
- 若要減緩閃爍的效果，可以先把link標籤或者style標籤都放在所有DOM節點之前，比如head標籤內部。


#### 瀏覽器對於css的載入順序
- 瀏覽器對於css的載入順序：
	- 在HTML中，若於所有dom節點之前沒先在HTML載入css的話，會被瀏覽器認為沒有樣式要載入，導致它會以預設樣式內容來渲染
	- 在HTML中，若於所有dom節點之前先在HTML載入css的話，瀏覽器的渲染會往後挪，直到後續的CSSOM和DOM產出而結合成Rendering Tree來渲染
- 在HTML中，若於所有dom節點之前沒先在HTML載入css的話，會被瀏覽器認為沒有樣式要載入，導致它會以預設樣式內容來直接渲染，請問為何會這樣？ 原因為 `因為瀏覽器此時認為沒特製的CSSOM要弄，所以它只好以預設的內容來做
- 在HTML中，若於所有dom節點之前先在HTML載入css的話，瀏覽器的渲染會往後挪，直到後續的CSSOM和DOM產出而結合成Rendering Tree來渲染，請問為何會這樣？ 原因為 `因為瀏覽器此時認為會有特製的CSSOM要弄，所以會先阻塞瀏覽器的後續渲染，好讓CSSOM能正常和DOM結合成Rendering Tree`
###  CSSOM阻塞

> css会不会阻塞后面js执行？答案是会！
> 
> JS 的作用在于修改，它帮助我们修改网页的方方面面：内容、样式以及它如何响应用户交互。这“方方面面”的修改，本质上都是对 DOM 和 CSSDOM 进行修改。当在JS中访问了CSSDOM中某个元素的样式，那么这时候就需要等待这个样式被下载完成才能继续往下执行JS脚本。

> 运行下面这个例子，就会发现等css加载完成后，才会在控制台打印“this is a test”。
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" type="text/css" href="https://h5.sinaimg.cn/m/weibo-pro/css/chunk-vendors.d6cac585.css">
</head>
<body>
  <div class="woo-spinner-filled">hello world</div>
  <div>hello world2</div>
  <script>
    console.log('this is a test')
  </script>
</body>
</html>
```

重點：
- CSSOM的建構任務會阻塞JS執行
- 由於JS本身會修改DOM 和 CSSOM：
	- DOM：瀏覽器會從邊接收內容邊解析成DOM，換言之，只要能接收到一部分內容就會有DOM
	- CSSOM：瀏覽器會先接收整份內容並解析成CSSOM，不會邊接收內容而邊解析成CSSOM，換言之，在還沒有處理完之前，都不會有CSSOM
	- 由於CSS本身在還沒處理完之前是不會有CSSOM，為了確保JS能夠使用到CSSOM，會讓CSSOM建構任務阻塞JS。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661871513/blog/cssTag/css-blocking/standard-css-block-js_m6u3pj.png)

## 複習

#🧠 HTML、Javascript以及 CSS 在同一個HTML DOM文件的阻塞關係為何？>->-> `> 1.  Javascript 會阻擋 DOM 的建構 2.  CSS 會阻擋 Javascript 的執行 3.  CSS 會影響頁面的 Rendering`
<!--SR:!2022-12-24,74,250-->

#🧠 同一份DOM文件的載入，為何CSSOM會阻塞渲染？->->-> `由於CSS本身在還沒處理完之前是不會有CSSOM，為了確保Rendering能夠使用到CSSOM，會讓CSSOM建構任務阻塞JS。`
<!--SR:!2024-05-17,375,250-->

#🧠 同一份DOM文件的載入，CSSOM會導致什麼的阻塞 ->->-> `1.  CSS 會阻擋 Javascript 的執行 2.  CSS 會影響頁面的 Rendering`
<!--SR:!2023-09-25,142,230-->

#🧠 同一份DOM文件的載入，為何CSSOM要阻塞JS?  ->->-> `由於CSS本身在還沒處理完之前是不會有CSSOM，為了確保JS能夠使用到CSSOM，會讓CSSOM阻塞JS。`
<!--SR:!2024-10-18,472,250-->


#🧠 當瀏覽器的HTML 解析器解析HTML內容，若發現 link標籤或者style標籤時，如果是指定CSS檔案，會做什麼？ ->->-> `就會生成非同步任務A去負責載入CSS檔案、解析其內容轉成CSSOM、以該CSS來作為CSSOM的主要內容`
<!--SR:!2024-04-28,249,230-->

#🧠 當瀏覽器的HTML 解析器解析HTML內容，若發現 link標籤或者style標籤時，如果是指定CSS檔案，會做什麼？ (重複)->->-> `就會生成非同步任務A去負責載入CSS檔案、解析其內容轉成CSSOM、以該CSS來作為CSSOM的主要內容`
<!--SR:!2024-01-14,145,227-->


#🧠 CSSOM的構建任務會不會阻塞DOM的建立 ->->-> `不會`
<!--SR:!2024-04-17,366,250-->

#🧠 在正常情況下，HTML解析成DOM之後，會做什麼？ ->->-> `就會搭配CSSOM來打造Rendering Tree，接著執行渲染內容的任務(layout & paint)`
<!--SR:!2024-05-18,376,250-->

#🧠 HTML解析成DOM之後會搭配，CSSOM來打造Rendering Tree，接著執行渲染內容的任務(layout & paint)，那麼若CSSOM還未建立完成的話 ->->-> `就會阻塞打造Rendering Tree以及後續的渲染任務，直到CSSOM建立完成`
<!--SR:!2024-07-24,425,250-->

#🧠 HTML解析成DOM之後會搭配，CSSOM來打造Rendering Tree，接著執行渲染內容的任務(layout & paint)，那麼若CSSOM還未建立完成的話，那就會就會阻塞打造Rendering Tree以及後續的渲染任務，如何做才會繼續停止阻塞？ ->->-> `直到CSSOM建立完成`
<!--SR:!2025-02-13,544,250-->

#🧠 瀏覽器會不會給予每個HTML DOM節點設定預設的selector樣式，具體的selector是以什麼形式 ->->-> `會是以type selector來設定`
<!--SR:!2023-10-19,148,230-->

#🧠   請問這會引發什麼問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661937279/blog/cssTag/flash-problem_i3dfmz.png) ->->-> `若遇到link標籤或者style標籤之前就有DOM，那麼瀏覽器會在那之前執行該DOM結構上的渲染內容使其出現畫面，接著讀取DOM之後的link標籤或者style標籤的話，就會觸發CSSOM的建立任務，而當完成之後，會重新刷新DOM之前的畫面，這時會有閃爍的效果`
<!--SR:!2024-04-17,239,230-->


#🧠  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661937279/blog/cssTag/flash-problem_i3dfmz.png) 這會引發閃爍問題，請問如何解決？ ->->-> `將link標籤或者style標籤都放在所有DOM之前，比如head標籤`
<!--SR:!2023-12-13,108,230-->

#🧠  若遇到link標籤或者style標籤之前就有DOM，瀏覽器會如何處理？->->-> ` 若遇到link標籤或者style標籤之前就有DOM，因爲它會認為沒有樣式要載入，所以就以預設的設定就先渲染`
<!--SR:!2023-10-03,92,230-->


#🧠 在HTML中，若於所有dom節點之前載入css的話，其瀏覽器的渲染會如何做？ ->->-> `若先在HTML載入css的話，瀏覽器的渲染會往後挪，直到CSSOM和DOM都能產生出來`
<!--SR:!2023-10-13,245,250-->

#🧠 在HTML中，若於所有dom節點之前沒先在HTML載入css的話，其瀏覽器的渲染會如何做？ ->->-> `會被瀏覽器認為沒有樣式要載入，導致它會以預設樣式內容來直接渲染`
<!--SR:!2025-03-03,556,250-->

#🧠  在HTML中，若於所有dom節點之前沒先在HTML載入css的話，它會以預設樣式內容來直接渲染，請問為何？ ->->-> `因為瀏覽器此時認為沒特製的CSSOM要弄，所以它只好以預設的內容來做`
<!--SR:!2025-03-03,560,250-->


#🧠 在HTML中，若於所有dom節點之前載入css的話，瀏覽器的渲染會往後挪，直到後續的CSSOM和DOM產出而結合成Rendering Tree來渲染，請問為何會這樣？ ->->-> `因為瀏覽器此時認為會有特製的CSSOM要弄，所以會先阻塞瀏覽器的後續渲染，好讓CSSOM能正常和DOM結合成Rendering Tree`
<!--SR:!2024-10-11,469,250-->




---
Status: #🌱 
Tags:
[[JavaScript]] - [[CSS]]
Links:
[[客戶端利用link標籤或者style標籤來解析CSS檔案內容為CSSOM會是以接收完整份CSS檔案才開始解析成CSSOM，而非邊接收邊解析成CSSOM]]
References:
[[@ithome30TianXueHuiWeb]]
https://juejin.cn/post/6984658863735701517