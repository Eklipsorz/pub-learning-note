
## 描述



Route元件的loader通常要求什麼樣的loader?
`回傳一個負責資料索求請求的函式物件`，當Route設定好時，只要使用者切換至對應path，React-router就會先執行loader來索求資料並於獲得資料時，在來將資料轉移至對應元件來渲染

Route元件的action通常要求什麼樣的action?
	`本身能夠回傳回應封包或者回應資料的函式物件`，當Route設定好時，只要在該Route對應的元件觸發特定動作就會透過導向至action所在的path來執行對應action


#🧠 react-router v6.4：Route元件的loader通常要求什麼樣的loader? ->->-> `回傳一個promise為主的資料索求請求的函式物件`
<!--SR:!2023-03-17,60,250-->


## 複習

#🧠 react-router-v6.4：Route元件的loader通常要求什麼樣的loader? ->->-> `回傳一個負責資料索求請求的函式物件`
<!--SR:!2023-03-31,69,250-->

#🧠 react-router-v6.4：Route元件的action通常要求什麼樣的action?->->-> `本身能夠回傳回應封包或者回應資料的函式物件`
<!--SR:!2023-01-23,28,250-->

#🧠 react-router-v6.4：當Route設定好loader時，會如何執行？ ->->-> `只要使用者切換至對應path，React-router就會先執行loader來索求資料並於獲得資料時，在來將資料轉移至對應元件來渲染`
<!--SR:!2023-04-01,70,250-->

#🧠 react-router-v6.4：當Route設定好action時，會如何執行？->->-> `當Route設定好時，只要在該Route對應的元件觸發特定動作就會透過導向至action所在的path來執行對應action`
<!--SR:!2023-03-10,55,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References: