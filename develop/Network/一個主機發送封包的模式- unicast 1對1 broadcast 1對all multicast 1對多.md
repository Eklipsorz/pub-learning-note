
## 描述

### cast 含義
根據 [[@vivekreddyDifferenceUnicastBroadcast]]所描述的unicast、multicast、broadcast之間的差別：

> The **cast** term here signifies some data(stream of packets) is being transmitted to the recipient(s) from the client(s) side over the communication channel that helps them to communicate.

重點：
- cast 會是指傳送方傳送資料至接收方的動詞、行為名詞
	- 傳送方可以是由一個或多個傳送方所構成
	- 接收方可以是由一個或多個接收方所構成




### Unicast 
引用[[@dineshWhatUnicastBroadcast]]所描述的unicast定義


> Unicast is a type of communication where data is sent from one computer to another computer. In Unicast type of communication, there is only one sender, and one receiver.

unicast：
- 泛指傳送方和接收方都各為一個，這兩方所處的網路可以是一樣或者不一樣
- 換言之，一個傳遞方A傳遞資訊至另一個接收方B

### Broadcast
> Broadcast is a type of communication where data is sent from one computer once and a copy of that data will be forwarded to all the devices.  

[[@DifferenceBroadcastMulticast]]
> Broadcast transfer (one-to-all) techniques and can be classified into two types : Limited Broadcasting, Direct Broadcasting. In broadcasting mode, transmission happens from one host to all the other hosts connected on the LAN. The devices such as bridge uses this. The protocol like ARP implement this, in order to know MAC address for the corresponding IP address of the host machine. ARP does ip address to mac address translation. RARP does the reverse.

![](https://media.geeksforgeeks.org/wp-content/uploads/20201026202439/broadcast.png)

broadcast ：
- 
- 指一旦某個主機A發送封包，就會是以該封包內容作為副本來向指定網路下的所有主機發送封包
- 指定網路可以是主機A所在的網路，或者其他網路

###  Multicast
> Multicast is a type of communication where multicast traffic addressed for a group of devices on the network. IP multicast traffic are sent to a group and only members of that group receive and/or process the Multicast traffic.

[[@DifferenceBroadcastMulticast]]
> Multicasting has one/more senders and one/more recipients participate in data transfer traffic. In multicasting traffic recline between the boundaries of unicast and broadcast. It server’s direct single copies of data streams and that are then simulated and routed to hosts that request it. IP multicast requires support of some other protocols such as IGMP (Internet Group Management Protocol), Multicast routing for its working. And also in Classful IP addressing Class D is reserved for multicast groups.

![](https://media.geeksforgeeks.org/wp-content/uploads/20201026205734/Multicast.png)

Multicast ：
- 是指一個主機向一組由指定網路下的群組發送封包
- 群組會由多個在指定網路下的主機所構成
- 由於群組下的主機數量不一定會是指定網路的所有主機，因此和Broadcast 有所區別
- 指定網路可以是主機A所在的網路，或者其他網路

## 總結
引用[[@dineshWhatUnicastBroadcast]]: 
![[https://techiemaster.files.wordpress.com/2016/08/slide_6.jpg?w=816]]

重點：
- unicast、broadcast、multicast 描述著一個綁定IP的主機傳播封包的形式
- unicast: 一個電腦主機 會向另一個電腦主機發送封包。
- broadcast: 一個主機 會向指定網路下的所有主機發送封包。
- multicast: 一個主機 會向指定群組下的所有主機發送封包，由多個主機構成一個指定群組，其主機數量不一定會是某個特定網路的所有主機。

## Note 

1. cast 原意為動詞，以特定方向去投射光或影
> **to send light or shadow (= an area of darkness) in a particular direction**


2. uni- ：作為字首(prefix)，強調著單一、單獨、一
> **having or consisting of only one**


3. multi-：作為字首，強調多個、許多、多
>**having many**

4. broad：原意為形容詞，形容寬廣的。
> **very wide**

## 複習

#🧠 Question unicast、broadcast、multicast中的cast是指 ->->-> `cast 指的是從(一個/多個)客戶端發送資料至(一個/多個)接收方 的行爲`
<!--SR:!2023-01-14,145,250-->

#🧠 Question Unicast 是什麼樣的傳播方式？->->-> `在網路傳遞中，只會有一個主機A傳遞資訊至另一個主機B，也就是說只會有一個傳送者和一個接收者`
<!--SR:!2023-10-22,313,250-->


#🧠 Broadcast 是什麼樣的傳播方式？ ->->-> `指一旦某個主機A發送封包，就會是以該封包內容作為副本來向指定網路下的所有主機發送封包`
<!--SR:!2023-04-09,179,230-->


#🧠 Multicast  是什麼樣的傳播方式？->->-> `是指一個主機向一組由指定網路下的群組發送封包，群組會由多個在指定網路下的主機所構成，由於群組下的主機數量不一定會是指定網路的所有主機，因此和Broadcast 有所區別`
<!--SR:!2022-12-25,133,250-->

---
Status: #🌱 
Tags:
[[Network]]
Links:
[[分類定址是將IP分個群組來重新定義使用者能用的IP群組是什麼]]
References:
[[@dineshWhatUnicastBroadcast]]
[[@vivekreddyDifferenceUnicastBroadcast]]
