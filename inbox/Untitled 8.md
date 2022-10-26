## 描述



### webpage
[[@WebPageWikipedia]]
> A web page (or webpage) is a hypertext document on the World Wide Web. Web pages are delivered by a web server to the user and displayed in a web browser

> An HTML document can include Cascading Style Sheets (CSS) documents to describe the presentation of content on a web page. It can also include JavaScript or WebAssembly programs, which are executed by the web browser to add dynamic behavior to the web page.[2][3] Web pages with dynamic behavior can function as application software, referred to as web applications. 


重點：
- webpage 或者 page 本身會是指在網頁能夠呈現的hypertext 文件
- 每一份webpage文件都包含JS、CSS、HTML等形式的內容
- webpage 通常會是由網頁伺服器提供客戶端，並由客戶端解析並呈現成畫面




### SPA (Single Page Application)

> The core difference between a SPA and a MPA is that with a single-page application, all the requests happen within the lifecycle of a single HTML page. You might be able to see different views, even see different "pages" of the application, but all the rendering takes place within a single HTML web page. This has the advantage of keeping the state of the "application" all in one scope.


重點：
- Single Page Application 是以一個 實體 webpage 檔案為主體的應用程式
- 該應用程式的 "Page" 都會是透過對著webpage進行互動而產生出來，並且這些Page 相對於實體webpage檔案來說，是一個虛擬的webpage
- 所有對於網頁的請求都只會在這個單一webpage檔案的life cycle進行處理


### MPA (Multiple Page Application)

> An MPA, by contrast, will have the user visiting multiple distinct HTML pages. All scripts will be re-executed when the new HTML page loads and any state must be persisted in the session or in local storage. This is more like stackoverflow.com's model.

重點：




## 複習


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@WebPageWikipedia]]