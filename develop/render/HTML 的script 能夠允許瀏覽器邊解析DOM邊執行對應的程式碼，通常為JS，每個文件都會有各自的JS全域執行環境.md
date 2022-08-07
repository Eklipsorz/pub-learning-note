

## 描述
[[@mdnScriptElementHTML]] 所描述
```
The <script> HTML element is used to embed executable code or data; this is typically used to embed or refer to JavaScript code.
```

使用方式1
```
<script src="javascript.js"></script>
```

使用方式2
```
<script>
  alert("Hello World!");
</script>
```

[[@HTMLScriptTag]] 所描述
```
The `<script>` tag is used to embed a client-side script (JavaScript).

The `<script>` element either contains scripting statements, or it points to an external script file through the src attribute.

Common uses for JavaScript are image manipulation, form validation, and dynamic changes of content.
```

[[@JavaScriptScope]] 所描述：全域環境
> With JavaScript, the global scope is the JavaScript environment. 
> 
> In HTML, the global scope is the window object.
> 
> Global variables defined with the `var` keyword belong to the window object:

[[@mdnWindowWebAPIs]] 所描述的window物件：
> The Window interface represents a window containing a DOM document; the document property points to the DOM document loaded in that window.

> [`Window.document`](https://developer.mozilla.org/en-US/docs/Web/API/Window/document) Read only 
> Returns a reference to the document that the window contains.


> In a tabbed browser, each tab is represented by its own `Window` object; the global `window` seen by JavaScript code running within a given tab always represents the tab in which the code is running. That said, even in a tabbed browser, some properties and methods still apply to the overall window that contains the tab

重點：
- HTML 檔案下會有script標籤，來定義邊解析HTML時可以邊額外執行的程式碼或者可存取的資料，其程式碼會是以瀏覽器能夠解析並執行的為主，比如JavaScript
```
<script>...</script>
```
- 在同份檔案下，script 標籤具有兩種形式可以使用
	- 調用對應腳本檔案
	```
	<script src="javascript.js"></script>
	```
	- 實際在script標籤內定義要執行什麼樣的指令
	```
	<script>
	  // 指令
	  alert("Hello World!");
	</script>
	```

- 當瀏覽器讀取到JS時，就會開始解析並執行對應的JS語言：
	-  同一份DOM Document 會經由瀏覽器分析成以window實例物件構成的BOM
	-  首次執行JS程式碼時，會建立全域物件為window物件的Global Execution Context並記錄當時JS程式碼的識別字和對應實體物件
	- 後面執行的JS程式碼會延續著前面建立的GEC來執行並刷新識別字的對應實體物件內容
	- 同一份DOM Document載入的多個JS檔案會因為同一份的DOM Document所產生出來的同個GEC而讓多個JS檔案在同一個全域環境上執行，
- 每一個DOM document都有各自不同的Window 物件，透過window物件來決定GEC歸屬於誰，所以每個DOM document所對應的全域環境都會是不同，同份document 執行的JS程式碼會以相同的全域環境執行
- 瀏覽器可允許多個標籤頁，每個標籤頁都對應一個畫面，每個標籤頁都對應不同的window物件，那麼彼此間的JavaScript全域環境並不會共享

## 複習
#🧠 當瀏覽器讀取到JS時，瀏覽器會如何做？ ->->-> `當瀏覽器讀取到JS時，就會開始解析並執行對應的JS語言`
<!--SR:!2022-08-22,23,250-->


#🧠 JS語言上在瀏覽器上的全域環境是什麼？(GEC) ->->-> `其JS語言的全域環境會是以目前的Window物件內容為主來從而構成對應的GEC，並以GEC來輔助執行同一個DOM document上的JS代碼`
<!--SR:!2022-08-13,6,248-->

#🧠 JS語言上在瀏覽器上的全域環境是什麼？->->-> `其JS語言的全域環境會是以目前的Window物件內容為主來從而構成對應的GEC，並以GEC來輔助執行同一個DOM document上的JS代碼`
<!--SR:!2022-08-13,6,248-->


#🧠 每一個DOM document 對於Window物件來說，是指多個document共享同一個window物件？還是每個document 都有各自的window物件？ 為什麼？(GEC)->->-> `每一個DOM document都有各自的Window 物件：DOM document會是經由瀏覽器解析成另一個window 物件所構成的DOM tree，而JS語言的全域環境會是以目前的Window物件內容為主來構建GEC，而由同一個window物件構成GEC來執行同一個DOM document上的JS代碼`
<!--SR:!2022-08-13,6,248-->

#🧠 每一個DOM document 對於Window物件來說，是指多個document共享同一個window物件？還是每個document 都有各自的window物件？ 為什麼？->->-> `每一個DOM document都有各自的Window 物件：DOM document會是經由瀏覽器解析成另一個window 物件所構成的DOM tree，而JS語言的全域環境會是以目前的Window物件內容為主來構建GEC，而由同一個window物件構成GEC來執行同一個DOM document上的JS代碼`
<!--SR:!2022-08-08,1,228-->


#🧠 假設有兩個HTML檔案，裡面有各自JS腳本程式碼，請問他們的全域變數會是共享的？ ->->-> `並不會，因為每個HTML檔案都會被解析成各自不同的window物件，而每個window物件會構成不同的GEC，這兩個檔案的全域環境是不同，且兩者的變數並不會共享的`
<!--SR:!2022-08-22,23,250-->

#🧠 若瀏覽器可允許使用者開啟多個標籤頁，每個標籤頁都對應一個畫面，那麼對於window物件和javascript全域環境來說，是代表什麼？ ->->-> `每個標籤頁都對應不同的window物件，那麼就會有兩個不同的GEC，那麼彼此間的JavaScript全域環境並不會共享`
<!--SR:!2022-08-13,6,248-->


#🧠 同一個HTML檔案中，JavaScript有哪些寫法？ ->->-> `<script src="javascript.js"></script> 和 <script>指令</script>`
<!--SR:!2022-08-19,20,250-->


#🧠  HTML 檔案下會有script標籤是做什麼？ ->->-> `來定義邊解析HTML時可以邊額外執行的程式碼或者可存取的資料，其程式碼會是以瀏覽器能夠解析並執行的為主，比如JavaScript`
<!--SR:!2022-08-23,16,230-->



---
Status: #🌱  
Tags: 
[[HTML]] - [[JavaScript]]
Links:
[[parser blocking 是瀏覽器的HTML內容解析器因特定原因而被其他元件給停止解析，render blocking 是瀏覽器的渲染器元件因特定原因而被其他元件給停止渲染]]
[[html 上的script 添加defer、async可使script提供asynchronous loading功能，都沒添加則以synchronous loading為主]]
References:
[[@JavaScriptScope]]
[[@HTMLScriptTag]]
[[@mdnScriptElementHTML]]
[[@mdnWindowWebAPIs]]