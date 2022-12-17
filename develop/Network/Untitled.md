## 描述

[[@Anycast2022]]
> delivers a message to any one out of a group of nodes, typically the one nearest to the source using a one-to-one-of-many[1] association where datagrams are routed to any single member of a group of potential receivers that are all identified by the same destination address. The routing algorithm selects the single receiver from the group based on which is the nearest according to some distance or cost measure.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Anycast.svg/1024px-Anycast.svg.png)
重點：
- anycast：意指為一個傳遞方傳遞資料至可任意選擇一個接收方的群組，而群組內會有N個接收方。
	- 應用為：
		- routing algorithm：ㄐㄩ將N個接收方設定為相同的IP，並且根據傳遞方和接收方之間的距離、傳遞狀況來決定傳遞方要跟哪個接收方進行傳遞、接收、處理


## 複習
#🧠 anycast 是什麼樣的概念 ->->-> `為一個傳遞方傳遞資料至可任意選擇一個接收方的群組`

#🧠 anycast 是為一個傳遞方傳遞資料至可任意選擇一個接收方的群組，其中群組內的接收方數量為何 ->->-> `N個`


#🧠 anycast為一個傳遞方傳遞資料至可任意選擇一個接收方的群組之概念，其應用為何 ->->-> ``



---
Status: #🌱 
Tags:
[[Network]]
Links:
References:
[[@Anycast2022]]
