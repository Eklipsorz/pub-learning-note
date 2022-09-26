## 描述

> empty wrapper component：It doesn't render any real HTML element to the DOM. But it fulfills React's/JSX requirement


重點：
- empty wrapper component ：
	- 指實質上不會有任何對應Virtual DOM和對應實際DOM節點
	- 憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件。
- 實現：
[[React：製作empty wrapper component來替代原本要用div包含的子節點，該wrapper component實際上對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構]]

## 複習
#🧠 empty wrapper component 在React 中是什麼？ ->->-> `指實質上不會有任何對應Virtual DOM和對應實際DOM節點，憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件。`
<!--SR:!2022-10-22,28,250-->

#🧠 使用React原生語法來建立Virtual DOM和對應，要載入react函式庫嗎？ ->->-> `要`
<!--SR:!2022-09-29,3,250-->

#🧠 哪種情況下，需要載入react函式庫，假如不載入hook的話，是React原生語法？還是JSX? ->->-> `React原生語法`
<!--SR:!2022-09-29,3,250-->

#🧠 empty wrapper component 在React 中會有對應的Virtual DOM嗎？ ->->-> `沒有`
<!--SR:!2022-10-22,28,250-->

#🧠 empty wrapper component 在React 中會有對應的real DOM嗎？ ->->-> `沒有`
<!--SR:!2022-10-22,28,250-->

#🧠 empty wrapper component 在React 中如何滿足JSX的侷限問題？ ->->-> `依據著對於createElement語法上的合法性來產出一個empty wrapper component，該wrapper component會包含多個子節點`
<!--SR:!2022-10-22,28,250-->

#🧠 JSX語法上的侷限就一定是React本身無法做到的嗎？ ->->-> `並不是，純粹是語法糖的轉換問題`
<!--SR:!2022-10-22,28,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]
References: