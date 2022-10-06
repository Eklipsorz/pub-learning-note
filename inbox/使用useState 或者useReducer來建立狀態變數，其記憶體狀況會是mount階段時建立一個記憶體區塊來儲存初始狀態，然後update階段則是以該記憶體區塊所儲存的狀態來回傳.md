## 描述

使用useState 或者useReducer來建立狀態變數：
- 在對應元件的mount階段時，會將狀態的初始值設定在React體系所管理的記憶體區塊中負責儲存狀態的部分
- 隨後對應元件的update階段，會直接透過setState或者reducer來將指定狀態值更新至其記憶體區塊，以便之後從該記憶體區塊取得內容


## 複習

#🧠 React：使用useState 或者useReducer來建立狀態變數， 其記憶體狀況整體會是什麼？(請以mount階段和update階段來說明)->->-> `在對應元件的mount階段時，會將狀態的初始值設定在React體系所管理的記憶體區塊中負責儲存狀態的部分、隨後對應元件的update階段，會直接透過setState或者reducer來將指定狀態值更新至其記憶體區塊，以便之後從該記憶體區塊取得內容`

#🧠 React：使用useState 或者useReducer來建立狀態變數， 在對應元件的mount階段下，其記憶體狀況整體會是什麼？->->-> `在對應元件的mount階段時，會將狀態的初始值設定在React體系所管理的記憶體區塊中負責儲存狀態的部分`

#🧠 React：使用useState 或者useReducer來建立狀態變數， 在對應元件的update階段下，其記憶體狀況整體會是什麼？ ->->-> `隨後對應元件的update階段，會直接透過setState或者reducer來將指定狀態值更新至其記憶體區塊，以便之後從該記憶體區塊取得內容`

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
[[React：setState從要求更改狀態至完成狀態改變&渲染之間是有時間差，若面對大量更改狀態要求的情況下，會使得時間差加重]]
References: