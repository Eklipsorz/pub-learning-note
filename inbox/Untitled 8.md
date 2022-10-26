## 描述



### webpage
[[@WebPageWikipedia]]
> A web page (or webpage) is a hypertext document on the World Wide Web. Web pages are delivered by a web server to the user and displayed in a web browser

> The core element of a web page is a text file written in the HyperText Markup Language (HTML)

> An HTML document can include Cascading Style Sheets (CSS) documents to describe the presentation of content on a web page. It can also include JavaScript or WebAssembly programs, which are executed by the web browser to add dynamic behavior to the web page.[2][3] Web pages with dynamic behavior can function as application software, referred to as web applications. 


重點：
- webpage 或者 page 本身會是指存在網際網路上的hypertext 文件，而網際網路則是意旨為分散各地的電腦主機透過網路設備組織而成的大型網路架構
- 具體來說，每一份webpage文件的主體會是包含JS、CSS的HTML檔案
- webpage 通常會是由網頁伺服器提供客戶端，並由客戶端解析並呈現成畫面，換言之，每個webpage代表著對應畫面。




### SPA (Single-Page Application)


> The core difference between a SPA and a MPA is that with a single-page application, all the requests happen within the lifecycle of a single HTML page. You might be able to see different views, even see different "pages" of the application, but all the rendering takes place within a single HTML web page. This has the advantage of keeping the state of the "application" all in one scope.


重點：
- Single Page Application 概念上是以一個 實體 webpage 檔案為主體而構成的應用程式
- 該應用程式的 每個"Page" 都會是透過對著webpage進行互動而產生出來，並且這些Page 相對於實體webpage檔案來說，是一個虛擬的webpage
- 所有對於網頁的請求回應都只會在這個單一實體webpage檔案的life cycle進行處理
- 網頁上的狀態皆由單一實體webpage檔案來管理

### MPA (Multiple Page Application)

> An MPA, by contrast, will have the user visiting multiple distinct HTML pages. All scripts will be re-executed when the new HTML page loads and any state must be persisted in the session or in local storage. 

重點：
- Multiple Page Application 概念上是以多個 實體webpage 檔案為主體而構成的應用程式
- 該應用程式的 每個 "Page" 都是對應著不同的實體webpage檔案
- 所有對於網頁的請求回應都會在這些實體webpage檔案間進行
- 網頁上的狀態都依據page的不同來交由各自的page來管理


#### 額外細節
- MPA：當切換成頁面來載入，都會重新執行對應script

## 複習

#🧠 webpage 概念上是什麼？ ->->-> `本身會是指存在網際網路上的hypertext 文件`

#🧠 webpage 和 page有啥差別 ->->-> `並無差別`

#🧠 webpage  本身會是指存在網際網路上的hypertext 文件，具體來說->->-> `每一份webpage文件的主體會是包含JS、CSS的HTML檔案`

#🧠 webpage 會放在哪？又能做些什麼？->->-> `webpage 通常會是由網頁伺服器提供客戶端，並由客戶端解析並呈現成畫面，換言之，每個webpage代表著對應畫面。`

#🧠 Single-Page Application 概念上會是什麼？->->-> `是以一個 實體 webpage 檔案為主體而構成的應用程式`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``








---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@WebPageWikipedia]]