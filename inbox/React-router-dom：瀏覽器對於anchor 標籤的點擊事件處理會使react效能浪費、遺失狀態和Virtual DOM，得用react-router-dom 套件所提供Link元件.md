## 描述


### anchor 標籤 對於React的問題

瀏覽器對於anchor 標籤的點擊事件處理：對特定頁面端點發送請求來索要全新的webpage

對特定頁面端點發送請求來索要全新的webpage，相當於是要求React unmount目前畫面上的所有元件，並向指定path的對應component進行mount，因而衍生以下問題：
- 效能浪費：由於會直接地unmount目前所對應的元件，而不是針對元件之間的DOM差異來做渲染，所以會造成效能上的不必要浪費
- 失去原有的Virtual DOM和狀態：由於經歷unmount而釋放掉對應component所擁有的對應Virtual DOM、狀態等資訊

比如說若是放在購物車場景的話，並以購物項目為狀態，那麼這問題套用在這，會使得先前的購物項目全部遺失。

#### 錯誤案例

```
const MainHeader = () => {
  return (
    <header>
      <nav>
        <ul>
          <li>
            <a href='/welcome'>Welcome</a>
          </li>
          <li>
            <a href='/Products'>Products</a>
          </li>
        </ul>
      </nav>
    </header>
  );
};

export default MainHeader;
```


只要點選夾帶著welcome位置和products位置的anchor 標籤就向對應端點發送新請求來索要新的網頁
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666960857/blog/react/react-router/anchor-tag-welcome_scwbdu.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666960857/blog/react/react-router/anchor-tag-products_suhcrh.png)


### 解法概念
解決方式：
- 設定點擊事件，並取消掉對應的預設處理，接著再以自己預期的結果來實現
- 使用react-router-dom的Link component


### 使用react-router-dom的Link component

[[@react-routerReactRouterDeclarative]]

> Link ： 
> Provides declarative, accessible navigation around your application.

> to: string

> A string representation of the Link location, created by concatenating the location’s pathname, search, and hash properties.


react-router-dom Link ：
- 是一個component，提供hyperlink功能的component
- 本質上仍是\<a\>標籤所構成，其點擊事件處理會由react-router-dom來設定的點擊事件處理，處理會有：
	- 取消瀏覽器對於點擊事件的預設處理 
	- 再以DOM節點之間差異來從頁面1切換成頁面2
- 語法為：
	- to ： 要導向的頁面位置/網址
	- xxxx1：為被綁定網址/位置的hypertext
```
import { Link } from 'react-router-dom';

return (
	<Link to="xxxx">xxxx1</Link>
)
```

#### 案例

```
import { Link } from 'react-router-dom';

const MainHeader = () => {
  return (
    <header>
      <nav>
        <ul>
          <li>
            <Link to='/welcome'>Welcome</Link>
          </li>
          <li>
            <Link to='/Products'>Products</Link>
          </li>
        </ul>
      </nav>
    </header>
  );
};

export default MainHeader;
```

### anchor tag 
[[@AnchorElementHTML]]
> The \<a\> HTML element (or anchor element), with its href attribute, creates a hyperlink to web pages, files, email addresses, locations in the same page, or anything else a URL can address.

```
<a href="https://example.com">Website</a>
```

> href
>The URL that the hyperlink points to.


[[@danielwalkerWhyAreThey]]
> Originally anchor tags were used to link content within a specific large document (especially PDFs, not HTML pages), so a table of contents might contain internal anchor tags to the relative sections of the document, indexed by that table of content, for instance, and those relevant sections might contain links back to the table of contents - all within the same document. Thus the tag, acted like an anchor, dragging the view port across the document to it's point of anchor, like an anchor cable on a ship, dragging the ship across the surface of the sea to the point where the anchor was hitched. In fact, the animation that accompanied this action, often simulated this happening, to inform the user that this is what was taking place.



重點
- anchor element 的 anchor 用語是較為早期用法而命名的
	- 標籤就如同船上的錨那樣，可以會將整個viewport固定至對應網址的對應頁面上
- 具體是一種將特定頁面的網址/位置綁定在hypertext的標籤，當使用者與hypertext互動就會將使用者導向至特定頁面，以此實現hyperlink概念
- 用法：
	- href ：指定要導向哪個頁面的網址/位置
	- xxxx2 ：是要被綁定網址的hypertext
```
<a href='xxxx'>xxxx2</a> 
```
- 本身會具有瀏覽器設定的預設事件處理，比如點擊事件後，瀏覽器會重新會對對應端點發送新的請求來索求新的網頁

### anchor 命名緣由

> a heavy metal object, usually shaped like a cross with curved arms, on a strong rope or chain, that is dropped from a boat into the water to prevent the boat from moving away


重點：
- anchor：一種彎鉤狀的金屬物件，會搭配一條強壯繩索來讓金屬物件和船身相連，用途是透過金屬物件的彎鉤和繩子來將船身固定在某一點，不能移動 

## 複習

#🧠 anchor 命名緣由是什麼？ ->->-> `anchor：一種彎鉤狀的金屬物件，會搭配一條強壯繩索來讓金屬物件和船身相連，用途是透過金屬物件的彎鉤和繩子來將船身固定在某一點，不能移動`

#🧠 anchor element 的 anchor 會使element 變成何種意思？ ->->-> `標籤就如同船上的錨那樣，可以會將整個viewport固定至對應網址的對應頁面上`

#🧠 anchor element 的 anchor 就如同船上的錨那樣，可以會將整個viewport固定至對應網址的對應頁面上，具體會是->->-> `具體是一種將特定頁面的網址/位置綁定在hypertext的標籤，當使用者與hypertext互動就會將使用者導向至特定頁面`

#🧠 anchor element 標籤用法是什麼？->->-> `<a href='xxxx'>xxxx2</a> `

#🧠 anchor element 語法：\<a href='xxxx'\>xxxx2\<\/a\> 中的href 和 xxxx2為何？->->-> ` href ：指定要導向哪個頁面的網址/位置； xxxx2 ：是要被綁定網址的hypertext`

#🧠 anchor element 語法的預設事件處理中，常見的預設事件處理會是什麼事件？->->-> `點擊anchor element的事件`

#🧠 anchor element 語法的預設點擊事件是什麼？ ->->-> `點擊事件後，瀏覽器會重新會對對應端點發送新的請求來索求新的網頁`

#🧠 瀏覽器對於anchor element所實現的URL變動事件處理具體會是什麼？ ->->-> `點擊事件後，瀏覽器會重新會對對應端點發送新的請求來索求新的網頁`

#🧠 React：瀏覽器對於anchor 標籤的點擊事件處理：對特定頁面端點發送請求來索要全新的webpage，這對於React的component來說什麼，是什麼？請以unmount和mount來說明？ ->->-> `對特定頁面端點發送請求來索要全新的webpage，相當於是要求React unmount目前畫面上的所有元件，並向指定path的對應component進行mount`

#🧠 React：瀏覽器對於anchor 標籤的點擊事件處理，它為React帶來什麼樣的潛在問題？ ->->-> `效能浪費、失去原有的Virtual DOM和狀態`

#🧠 React：瀏覽器對於anchor 標籤的點擊事件處理，它為React帶來什麼樣的潛在問題？其中效能浪費是其中一個問題，具體說明 ->->-> `由於會直接地unmount目前所對應的元件，而不是針對元件之間的DOM差異來做渲染，所以會造成效能上的不必要浪費`

#🧠 React：瀏覽器對於anchor 標籤的點擊事件處理，它為React帶來什麼樣的潛在問題？其中失去原有的Virtual DOM和狀態是其中一個問題，具體說明 ->->-> `由於經歷unmount而釋放掉對應component所擁有的對應Virtual DOM、狀態等資訊`

#🧠 React：瀏覽器對於anchor 標籤的點擊事件處理，它為React帶來什麼樣的潛在問題？舉例說明？->->-> `比如說若是放在購物車場景的話，並以購物項目為狀態，那麼這問題套用在這，會使得先前的購物項目全部遺失。`

#🧠 ！[https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667047396/blog/react/react-router/react-router-wrong-example-with-anchor-element_fybsto.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667047396/blog/react/react-router/react-router-wrong-example-with-anchor-element_fybsto.png) ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References:
[[@AnchorElementHTML]]
[[@danielwalkerWhyAreThey]]