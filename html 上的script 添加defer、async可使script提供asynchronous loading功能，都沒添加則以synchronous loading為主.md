## 描述
[[@xiesongwuWoLiJieDeTongBuJiaZaiYuYiBuJiaZaiZhiHu]] 所描述
> -   **上面说javaScript是同步加载的不怎么好，css是异步加载的甚合我意，那么咱能不能把javaScript也给弄成异步加载的呢？不仅能，而且有两种方式:**

> 1.  **给script加上defer属性：  
>
```
<script defer src="script.js" ></script>  
```
    
> 有了defer属性之后，加载和渲染后续文档的过程将与script.js的加载一起进行，实现了javaScript与后续文档的异步加载，但script.js要在所有元素解析完成之后才开始执行.**
> 
> 2.  **给script加上async属性：  
```
	<script async src="script.js" ></script>  
```

> 有了async属性之后,加载和渲染后续文档的过程将与script.js的加载和执行同时进行,这也实现了javaScript与后续文档的异步加载,但async属性不能保证顺序,因为script.js加载好了就直接开始执行.**


[[@mdnScriptElementHTML]] 所描述：
> async
> 
> For classic scripts, if the async attribute is present, then the classic script will be fetched in parallel to parsing and evaluated as soon as it is available.


> defer
> 
> This Boolean attribute is set to indicate to a browser that the script is meant to be executed after the document has been parsed

重點：
- script 標籤沒添加任何強調使用asynchronous loading的語法，就以parser blocking形式來載入，而被載入的內容會是script所指定的代碼或者檔案。
[[parser blocking 是瀏覽器的HTML內容解析器因特定原因而被其他元件給停止解析，render blocking 是瀏覽器的渲染器元件因特定原因而被其他元件給停止渲染]]
- script 標籤上若添加defer或者async就即為使用asynchronous loading，而被載入的內容會是script所指定的代碼或者檔案。
	- \<script\> ：以parser blocking來載入，暫時停止瀏覽器目前的HTML內容解析，讓JS引擎獲取執行權，並讓引擎下載/加載script並執行script上的代碼，直到執行完畢後，才還原執行權給瀏覽器，讓它繼續解析HTML內容解析
	- \<script defer\> ：JS檔案或者JS Code的加載任務將會與前面解析網頁的任務同時間一起進行，但對應的JS執行必須要等所有DOM元素解析完成才開始執行
	- \<script async\>  ：JS檔案或者JS Code的加載任務仍會與前面解析網頁的任務同時間一起進行，但一旦JS檔案載入完就會立即開始執行JS
	
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659094553/blog/html/script-tag_lup7vy.png)



### asynchronous loading 命名緣由

asynchronous loading 是指任務內容為載入資訊至特定地方的任務，若每個載入資訊的任務不需要等待前任務完成就能執行任務的話，那麼就會是asynchronous loading
 
### synchronous loading  命名緣由
synchronous loading 是指任務內容為載入資訊至特定地方的任務，若每個載入資訊的任務需要等待前面任務完成才能執行任務的話，那麼就會是synchronous loading

## 複習
#🧠 asynchronous loading 是什麼？->->-> `是指任務內容為載入資訊至特定地方的任務，若每個載入資訊的任務不需要等待前任務完成就能執行任務的話，那麼就會是asynchronous loading`
<!--SR:!2022-08-08,10,250-->

#🧠 synchronous loading  是什麼？ ->->-> `是指任務內容為載入資訊至特定地方的任務，若每個載入資訊的任務需要等待前面任務完成才能執行任務的話，那麼就會是synchronous loading`
<!--SR:!2022-08-08,10,250-->

#🧠 在HTML檔案中，無添加defer或者無async的script，假設script是執行JS，那麼會是如何處理？ ->->-> `以parser blocking來載入，暫時停止瀏覽器目前的HTML內容解析，讓JS引擎獲取執行權，並讓引擎下載/加載script並執行script上的代碼，直到執行完畢後，才還原執行權給瀏覽器，讓它繼續解析HTML內容解析`
`

#🧠 在HTML檔案中，添加defer的script，假設script是執行JS ，那麼會是如何處理？->->-> `JS檔案或者JS Code的加載任務會與前面解析網頁的任務同時間一起進行，但對應的JS執行必須要等所有DOM元素解析完成才開始執行`


#🧠 在HTML檔案中，添加async的script，假設script是執行JS ，那麼會是如何處理？ ->->-> `JS檔案或者JS Code的加載任務會與前面解析網頁的任務同時間一起進行，但一旦JS檔案載入完就會立即開始執行JS`


#🧠 在HTML檔案中，無添加任何東西的script、添加defer的script、添加async的script， 哪一個是asynchronous loading?  ->->-> `添加defer的script是asynchronous loading、添加async的script是asynchronous loading`


#🧠 在HTML檔案中，添加defer的script和添加async的script兩者間差別為何，假設script是執行JS  ->->-> `前者一旦載入JS檔案，就會等渲染任務做完或者Document上的內容都被轉換成Rendering Tree，才會開始執行JS檔案；另一個則是只要載入好JS檔就立刻執行JS檔案`
<!--SR:!2022-08-08,10,250-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Rendering]]
Links:
[[synchronous 和 asynchronous 在電腦科學是分別指每個任務會等待前面任務完成才執行與每個任務都為獨立，不會等前面任務完成才執行]]
[[parser blocking 是瀏覽器的HTML內容解析器因特定原因而被其他元件給停止解析，render blocking 是瀏覽器的渲染器元件因特定原因而被其他元件給停止渲染]]
References:
[[@mdnScriptElementHTML]]
[[@xiesongwuWoLiJieDeTongBuJiaZaiYuYiBuJiaZaiZhiHu]]