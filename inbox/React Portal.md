## 描述
portals 是一個React 功能之一

> Portal 提供一個優秀方法來讓 children 可以 render 到 parent component DOM 樹以外的 DOM 節點。

為什麼不直接到目標位置render就好?
這是因爲想在發生事件的元件去觸發原本要ㄗㄞ


   
> Portal 是從 React 16 開始提供的功能，用來將元件渲染到父元件之外的 DOM 節點上。可以將 Portal 想像成，你 render 一個元件時，其實是改變頁面上某個地方的 DOM 結構。

> 你可能會想，那 Portal 是用在什麼情況？通常的 React 元件，你只能渲染在父元件下面，但如果你要寫一個 modal 對話框，或說父元件寫死了 overflow: hidden 或你遇到 z-index 的問題呢？這就是使用 Portal 的時候了！




Semantically and from a "clean HTML structure" perspective, having this nested modal isn't ideal. It is an overlay to the entire page after all (that's similar for side drawers, other dialogs etc.)

  

so logically, it's above everything else. and if it's then nested in some other HTML code, it might technically work because of styling,  but it's not a good structure

  

modal 邏輯上是要放在所有元件之上的元件來實現整個viewport的覆蓋效果，或許可以擺放至某些元件的內部，並且使用styling來實現覆蓋的效果，但這樣很容易讓人誤解該modal會不會只是覆蓋特定元件，而不是實現整個viewport的覆蓋效果

  

其他與modal類似效果的元件有：

- side drawer 側邊選單

- dialogues



這問題類似於將div元件打造成button，而非用button元件來打造

### portal 命名緣由

> A portal is a large impressive doorway at the entrance to a building.

> On the internet, a portal is a site that consists of links to other websites. 

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@reactPortalReact]]
