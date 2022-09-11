## 描述


[[@reactPortalReact]]
> Portal 提供一個優秀方法來讓 children 可以 render 到 parent component DOM 樹以外的 DOM 節點。


[[@fooishReactPortalReact]]
> Portal 是從 React 16 開始提供的功能，用來將元件渲染到父元件之外的 DOM 節點上。可以將 Portal 想像成，你 render 一個元件時，其實是改變頁面上某個地方的 DOM 結構。

> 你可能會想，那 Portal 是用在什麼情況？通常的 React 元件，你只能渲染在父元件下面，但如果你要寫一個 modal 對話框，或說父元件寫死了 overflow: hidden 或你遇到 z-index 的問題呢？這就是使用 Portal 的時候了！

> So that's the portal.  And the idea really just is that the rendered HTML content is moved somewhere else.



重點：
- portal 介面本身會是一個特定元件A的入口元件，在特定元件A掛載其他DOM節點的情況下，其他元件可以傳遞訊息至入口元件，而入口元件會間接傳遞至特定元件A並進行渲染。
- 問題背景為：
	- 元件A本身原本是在其他元件C下擔任子元件來渲染，而其他元件B想拿元件A進行狀態傳遞並做渲染，問題是元件A和元件B之間的關係不能夠確定是否parent-child關係，而難以進行狀態上的傳遞，即使可以，也會花一定成本來時間
- 功能：
	- 讓特定元件A掛載至其他實際DOM節點下，並於其他元件下建立入口元件，使其他元件透過入口元件來和特定元件A的實際DOM節點進行資訊傳遞和渲染。
解決了：
	-  為了很好地解決主要的問題背景，就在元件B建立一個元件A的入口元件，好讓元件B傳遞狀態至入口元件，而入口元件接收到資訊時就會轉遞至元件A，接著元件A根據資訊來渲染，好實現 元件A原本的目標 和 元件B想拿元件A進行狀態傳遞並做渲染。
	- 若特定元件A被parent元件的樣式寫死了，可建立portal介面，將特定元件A的對應實際DOM節點實際寫在特定實際DOM節點之下，這樣其特定元件A的樣式就不會被原本的parent 元件給鎖死。
細節：
	- Portal 不會破壞元件的渲染內容本身，但會轉移其實際DOM節點至指定地點

### portal 使用用法



使用React-DOM librar下的createPortal 來實現

```
import ReactDOM from 'react-dom';
// return a React Portal
ReactDOM.createPortal(children, container)
```

[[@reactPortalReact]]
> The first argument (`child`) is any renderable React child, such as an element, string, or fragment. The second argument (`container`) is a DOM element.

> 第一個參數（child）是任何可 render 的 React child，例如 element、string 或者 fragment。第二個參數（container）則是一個 DOM element。
  

重點：
- createPortal 引數：
	- 第一個引數：以JSX 語法為主，定義要渲染至特定實際DOM節點之下的的對應Virtual DOM內容
	- 第二個引數：以pointer為主，專門接收特定實際DOM節點的記憶體位址，通常使用DOM API來抓取其特定DOM節點的參照位置
- createPortal 回傳的是 react portal 介面

#### 使用案例




#### 使用createPortal 事前準備
請確保入口元件的對應元件要掛載的實際DOM節點是否存在webpack對應的網頁或者渲染網頁

##### modal 案例

modal 元件則是分為backdrop子元件和modal子元件，前者是背景，後者是modal本身，在這裡為了很好區分出這兩個子元件，才建立名為backdrop-root和modal-root這兩個實際DOM節點，好方便讓backdrop去掛載至backdrop-root下面以及讓modal掛載至modal-root的下面
```
1.  <body>
2.      <div id="backdrop-root"></div>
3.      <div id="modal-root"></div>
4.      <div id="root"></div>
5.  </body>
```

  
#### 使用的函式庫是react-dom
React library：React feature、state management
React-DOM library：控管React 對於DOM渲染介面的存取


  

### 適用場景 - modal/side drawer

> Semantically and from a "clean HTML structure" perspective, having this nested modal isn't ideal. It is an overlay to the entire page after all (that's similar for side drawers, other dialogs etc.)

> so logically, it's above everything else. and if it's then nested in some other HTML code, it might technically work because of styling,  but it's not a good structure

  
modal 邏輯上是要放在所有元件之上的元件來實現整個viewport的覆蓋效果，或許可以擺放至某些元件的內部，並且使用styling來實現覆蓋的效果，但這樣很容易讓人誤解該modal會不會只是覆蓋特定元件，而不是實現整個viewport的覆蓋效果

其他與modal類似效果的元件有：
- side drawer 側邊選單
- dialogues

然而modal為了很好與其他元件進行溝通，而會和其他元件寫在一塊，這樣很容易造成理解上的誤解以及樣式出錯。







### portal 命名緣由
portal：
> A portal is a large impressive doorway at the entrance to a building.

> On the internet, a portal is a site that consists of links to other websites. 

重點：
- portal 原意為建築物的主要入口
- 在網路裡，portal 會泛指著進入其他網頁的入口網頁

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@reactPortalReact]]
[[@fooishReactPortalReact]]
