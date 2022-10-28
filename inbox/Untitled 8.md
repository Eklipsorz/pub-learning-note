## 描述


### a 標籤問題

\<a\> 標籤將使用者導向至特定頁面：重新對特定頁面端點發送請求來索要全新的webpage，這樣子的處理方式正是瀏覽器對於URL變動的預設處理

  

這會導致什麼問題？

- 效能浪費

- 失去原有的VDOM和狀態：由於經歷unmount而釋放掉對應component所擁有的對應VDOM和狀態


比如說若是放在購物車場景的話，並以購物項目為狀態，那麼這問題套用在這，會使得先前的購物項目全部遺失。


### 解法
解決方式：

- 設定點擊事件，並取消掉對應的預設處理，接著再以自己預期的結果來實現

- 使用react-router-dom的Link component


### 使用react-router-dom的Link component
react-router-dom Link ：

- 是一個component，提供hyperlink功能的component

- 本質上仍是\<a\>標籤所構成，並綁定點擊事件處理來取消瀏覽器對於URL變動的預設處理，再以DOM節點之間差異來從頁面1切換成頁面2

- fake navigation


Link component

- to：指定要導向的端點是什麼？

### anchor tag 
[[@AnchorElementHTML]]
> The \<a\> HTML element (or anchor element), with its href attribute, creates a hyperlink to web pages, files, email addresses, locations in the same page, or anything else a URL can address.

```
<a href="https://example.com">Website</a>
```

> href
>The URL that the hyperlink points to.



> Originally anchor tags were used to link content within a specific large document (especially PDFs, not HTML pages), so a table of contents might contain internal anchor tags to the relative sections of the document, indexed by that table of content, for instance, and those relevant sections might contain links back to the table of contents - all within the same document. Thus the tag, acted like an anchor, dragging the view port across the document to it's point of anchor, like an anchor cable on a ship, dragging the ship across the surface of the sea to the point where the anchor was hitched. In fact, the animation that accompanied this action, often simulated this happening, to inform the user that this is what was taking place.



重點
- anchor element 的 anchor 用語是較為早期用法而命名的
	- 標籤就如同船上的錨那樣，可以會將整個viewport固定至對應網址的對應頁面上
- 具體是一種將特定頁面的網址/位置綁定在hypertext的標籤，當使用者與hypertext互動就會將使用者導向至特定頁面，以此實現hyperlink概念
- 用法：
	- href ：指定要導向哪個頁面的網址/位置
	- xxxx2 
```
<a href='xxxx'>xxxx2</a> 
```
- 本身會具有瀏覽器設定的預設事件處理，比如點擊事件後，瀏覽器會重新會對對應端點發送新的請求來索求新的網頁

### anchor 命名緣由

> a heavy metal object, usually shaped like a cross with curved arms, on a strong rope or chain, that is dropped from a boat into the water to prevent the boat from moving away


重點：
- anchor：一種彎鉤狀的金屬物件，會搭配一條強壯繩索來讓金屬物件和船身相連，用途是透過金屬物件的彎鉤和繩子來將船身固定在某一點，不能移動 

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References:
[[@AnchorElementHTML]]