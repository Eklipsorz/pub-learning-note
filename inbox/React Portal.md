## 描述
portals 是一個React 功能之一

Semantically and from a "clean HTML structure" perspective, having this nested modal isn't ideal. It is an overlay to the entire page after all (that's similar for side drawers, other dialogs etc.)

  

so logically, it's above everything else. and if it's then nested in some other HTML code, it might technically work because of styling,  but it's not a good structure

  

modal 邏輯上是要放在所有元件之上的元件來實現整個viewport的覆蓋效果，或許可以擺放至某些元件的內部，並且使用styling來實現覆蓋的效果，但這樣很容易讓人誤解該modal會不會只是覆蓋特定元件，而不是實現整個viewport的覆蓋效果

  

其他與modal類似效果的元件有：

- side drawer 側邊選單

- dialogues



這問題類似於將div元件打造成button，而非用button元件來打造
## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: