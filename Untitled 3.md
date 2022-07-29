## 描述



### parser blocking 
[[@ilyagrigorikAddingInteractivityJavaScript]] 所描述的
> When the HTML parser encounters a script tag, it pauses its process of constructing the DOM and yields control to the JavaScript engine; after the JavaScript engine finishes running, the browser then picks up where it left off and resumes DOM construction.

> By default, JavaScript execution is "parser blocking": when the browser encounters a script in the document it must pause DOM construction, hand over control to the JavaScript runtime, and let the script execute before proceeding with DOM construction.



[[@alohciAnswerParserBlocking2016]] 所描述：
> Imagine an HTML page has two `<script src="...">` elements. The parser sees the first one. It has to stop* parsing while it fetches and then executes the javascript, because it might contain `document.write()` method calls that fundamentally change how the subsequent markup is to be parsed. 
> 
> Fetching resources over the internet is comparatively much slower than the other things the browser does, so it sits waiting with nothing to do. Eventually the JS arrive, executes and the parser can move on. It then sees the second `<script src="...">` tag and has to go through the whole process of waiting for the resource to load again. It's a sequential process, and that's parser blocking.



重點：
- parser blocking：瀏覽器的HTML 內容解析器因特定原因而被其他元件阻塞
	- 原因會是：瀏覽器讀取到script，且script本身具有更改DOM節點的特性，為了避免破壞它是以現有的DOM狀況來實現/執行，所以會使瀏覽器停止解析並轉由JavaScript引擎來做後續JavaScript的解析和執行
	- 具體過程是：當瀏覽器在HTML上讀取到script且script是javascript時，它一定停止建構DOM 節點，並且將控制權轉交給JavaScript 引擎，讓引擎讀取script指定的javascript代碼來執行，等到引擎執行完畢，再由引擎將控制權轉交給瀏覽器，瀏覽器就回到當初被停止的地方繼續建構DOM。**瀏覽器因為讀取script而被迫停止解析HTML內容的現象就叫做parser blocking**


[[@alohciAnswerParserBlocking2016]] 所描述：
> CSS resources are different. When the parser sees a stylesheet to load, it issues the request to the server, and moves on. If there are other resources to load, these can all be fetched in parallel (subject to some HTTP restrictions). 
> 
> But only when the CSS resources are loaded and ready can the page be painted on the screen. That's render blocking, and because the fetches are in parallel, it's a less serious slow down.

重點：
- render blocking：瀏覽器的畫面渲染元件因特定原因而被其他原因阻塞
	- 原因會是：
	- 具體過程是：當瀏覽器在HTML上讀取到要載入的stylesheet，它就以非同步的形式去產生一個worker負責發送請求至stylesheet所在的主機上，並且同時間瀏覽器繼續做自己的內容解析，在這裡會有stylesheet的載入任務和瀏覽器內容解析同時在處理，但只有當stylesheet全被載入並準備繪製，瀏覽器才會開始依照DOM和CSS來繪製畫面，即使瀏覽器已經完成自己的內容解析也必須等待stylesheet完成準備繪製

> * Parser blocking is not quite as simple as that in some modern browsers. They have some ability to tentatively parse the following HTML in the hope that the script, when it loads and executes, doesn't do anything to mess up the subsequent parsing, or if it does, that the same resources are still required to be loaded. But they can still have to back out the work if the script does something awkward.


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@alohciAnswerParserBlocking2016]]
[[@ilyagrigorikAddingInteractivityJavaScript]]