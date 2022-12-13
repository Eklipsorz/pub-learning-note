
## 描述

Route元件的loader通常要求什麼樣的loader?
`回傳一個promise為主的資料索求請求的函式物件`，當Route設定好時，只要使用者切換至對應path，React-router就會先執行loader來索求資料並於獲得資料時，在來將資料轉移至對應元件來渲染

Route元件的通常要求什麼樣的action?
	`本身能夠回傳回應封包或者回應資料的函式物件`，當Route設定好時，只要在該Route對應的元件觸發特定動作就會透過導向至action所在的path來執行對應action


#🧠 react-router v6.4：Route元件的loader通常要求什麼樣的loader? ->->-> `回傳一個promise為主的資料索求請求的函式物件`


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: