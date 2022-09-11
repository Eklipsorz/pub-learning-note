## 描述
portals 是一個React 功能之一
[[@reactPortalReact]]
> Portal 提供一個優秀方法來讓 children 可以 render 到 parent component DOM 樹以外的 DOM 節點。

為什麼不直接到目標位置render就好?
元件A本身原本是在其他元件C下擔任子元件來渲染，而其他元件B想拿元件A進行狀態傳遞並做渲染，問題是元件A和元件B之間的關係不能夠確定是否parent-child關係，而難以進行狀態上的傳遞，即使可以，也會花一定成本來時間


為了很好地解決，就在元件B建立一個元件A的入口元件，好讓元件B傳遞狀態至入口元件，而入口元件接收到資訊時就會轉遞至元件A，接著元件A根據資訊來渲染，好實現 元件A原本的目標 和 元件B想拿元件A進行狀態傳遞並做渲染。

該portal會幫助元件A本身掛載在其他元件C上，

[[@fooishReactPortalReact]]
> Portal 是從 React 16 開始提供的功能，用來將元件渲染到父元件之外的 DOM 節點上。可以將 Portal 想像成，你 render 一個元件時，其實是改變頁面上某個地方的 DOM 結構。

> 你可能會想，那 Portal 是用在什麼情況？通常的 React 元件，你只能渲染在父元件下面，但如果你要寫一個 modal 對話框，或說父元件寫死了 overflow: hidden 或你遇到 z-index 的問題呢？這就是使用 Portal 的時候了！



Portal 為進入特定事物的入口，在React中會是指專做特定元件A的入口元件，一旦將資訊丟進入口元件，該入口元件會將資訊傳遞特定元件A來做其元件的渲染


Semantically and from a "clean HTML structure" perspective, having this nested modal isn't ideal. It is an overlay to the entire page after all (that's similar for side drawers, other dialogs etc.)

  

so logically, it's above everything else. and if it's then nested in some other HTML code, it might technically work because of styling,  but it's not a good structure

  

modal 邏輯上是要放在所有元件之上的元件來實現整個viewport的覆蓋效果，或許可以擺放至某些元件的內部，並且使用styling來實現覆蓋的效果，但這樣很容易讓人誤解該modal會不會只是覆蓋特定元件，而不是實現整個viewport的覆蓋效果

  

其他與modal類似效果的元件有：

- side drawer 側邊選單

- dialogues



這問題類似於將div元件打造成button，而非用button元件來打造

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
