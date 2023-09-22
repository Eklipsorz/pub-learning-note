
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
- broadcast 會是指一個傳送方A發送資料至特定網路下的所有主機
- 在broadcast概念中：
	- 傳送方和接收方兩者間的網路會是一樣或不一樣
	- 傳送方為一個，接收方為特定網路下的所有主機

###  Multicast
> Multicast is a type of communication where multicast traffic addressed for a group of devices on the network. IP multicast traffic are sent to a group and only members of that group receive and/or process the Multicast traffic.

[[@DifferenceBroadcastMulticast]]
> Multicasting has one/more senders and one/more recipients participate in data transfer traffic. In multicasting traffic recline between the boundaries of unicast and broadcast. It server’s direct single copies of data streams and that are then simulated and routed to hosts that request it. IP multicast requires support of some other protocols such as IGMP (Internet Group Management Protocol), Multicast routing for its working. And also in Classful IP addressing Class D is reserved for multicast groups.

![](https://media.geeksforgeeks.org/wp-content/uploads/20201026205734/Multicast.png)

Multicast ：
- multicast 會是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方：
	- N 和 M 會是至少1個
	- 特定群組A和特定群組B所在網路可以是不一樣或者一樣
	- 能夠構築的傳遞形式為：one-to-one、one-to-many、many-to-one、many-to-many
- one-to-many 形式為：1個傳送方傳送資料至特定群組的N個接收方
- many-to-one 形式為：位於特定群組A的N個傳送方傳送資料至特定群組B的1個接收方
- many-to-many 形式為：
	- 本身會是指one-to-many以及many-to-one的結合，意指為一個傳送方傳送資料至特定群組的N個接收方 和 多個傳送方傳送資料至同一個接收方 的合併行為
	- 具體為位處於群組A的N個傳送方傳送資料至另一個群組B的M個接收方
具體會是：
	- 藉由媒介來代表Receiver來接收多個Sender傳遞過來的訊息，接著再由媒介代表Sender轉發訊息至多個Receiver
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671281392/blog/network/transmission/many-to-many-transmission-example1_uaynks.png)

 - 一個傳遞方傳遞相同訊息至多個接收方；一個接收方會收到多個傳遞方所傳遞的訊息
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671281392/blog/network/transmission/many-to-many-transmission-example2_smbbs2.png)



## 總結
引用[[@dineshWhatUnicastBroadcast]]: 
![[https://techiemaster.files.wordpress.com/2016/08/slide_6.jpg?w=816]]

重點：
- unicast、broadcast、multicast 描述著一個綁定IP的主機傳播封包的形式
- unicast: 一個主機 會向另一個電腦主機發送封包。
- broadcast: 一個主機 會向指定網路下的所有主機發送封包。
- multicast: 指定群組A下的N個主機 會向指定群組B下的M個主機發送封包。

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



#🧠  unicast、broadcast、multicast中的cast是指 ->->-> `cast 會是指傳送方傳送資料至接收方的動詞、行為名詞`
<!--SR:!2024-06-20,332,250-->

#🧠 unicast、broadcast、multicast中的cast是指傳送方傳送資料至接收方的動詞、行為名詞，傳送方和接收方的數量為何？->->-> `傳送方和接收方的數量皆會是由一個或者多個`
<!--SR:!2024-06-21,333,250-->


#🧠 Unicast 是在網路傳遞中，只會有一個主機A傳遞資訊至另一個主機B，請問主機A和主機B的隸屬網路是什麼？->->-> `可以是一樣；可以是不一樣`
<!--SR:!2023-10-05,181,250-->

#🧠 Unicast 的傳遞方和接收方這兩者數量為何？ ->->-> `都各為1個`
<!--SR:!2024-06-22,334,250-->

#🧠  Unicast 是什麼樣的傳播方式？->->-> `在網路傳遞中，只會有一個主機A傳遞資訊至另一個主機B`
<!--SR:!2024-11-29,434,250-->

#🧠 Broadcast 是什麼樣的傳播方式？ ->->-> `一個傳送方A發送資料至特定網路下的所有主機`
<!--SR:!2024-09-12,384,250-->

#🧠 Broadcast 是一個傳送方A發送資料至特定網路下的所有主機的傳播方式，傳遞方和接收方的隸屬網路為何？ ->->-> `可以是一樣或者不一樣`
<!--SR:!2024-10-05,398,250-->

#🧠 Broadcast 是一個傳送方A發送資料至特定網路下的所有主機的傳播方式，傳遞方和接收方兩者間的數量為何？ ->->-> `傳送方為一個，接收方為特定網路下的所有主機`
<!--SR:!2023-10-13,186,250-->

#🧠 Multicast  是什麼樣的傳播方式？->->-> `multicast 會是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方`
<!--SR:!2024-03-20,220,230-->


#🧠  Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，其中的N和M皆為多少個，合併起來會是什麼意思->->-> `至少為1個`
<!--SR:!2024-05-18,314,250-->

#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，隸屬網路為何？ ->->-> `特定群組A和特定群組B所在網路可以是不一樣或者一樣`
<!--SR:!2023-10-09,183,250-->

#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，能夠構築的傳遞形式會是什麼？->->-> `one-to-one、one-to-many、many-to-one、many-to-many`
<!--SR:!2023-10-07,53,248-->


#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，能夠構築的傳遞形式會是什麼？其中的one-to-many會是什麼？ ->->-> `1個傳送方傳送資料至特定群組的N個接收方`
<!--SR:!2023-12-02,81,230-->



#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，能夠構築的傳遞形式會是什麼？其中的many-to-one會是什麼？->->-> `位於特定群組A的N個傳送方傳送資料至特定群組B的1個接收方`
<!--SR:!2023-10-05,180,250-->



#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，能夠構築的傳遞形式會是什麼？其中的many-to-many會是什麼？ ->->-> ` 具體為位處於群組A的N個傳送方傳送資料至另一個群組B的M個接收方`
<!--SR:!2023-10-27,197,250-->



#🧠 Multicast  是指位處於特定群組A的N個傳送方傳送資料至特定群組B的M個接收方，具體概念有哪兩種？ ->->-> `藉由媒介來代表Receiver來接收多個Sender傳遞過來的訊息，接著再由媒介代表Sender轉發訊息至多個Receiver、一個傳遞方傳遞相同訊息至多個接收方；一個接收方會收到多個傳遞方所傳遞的訊息`
<!--SR:!2023-11-11,180,230-->


#🧠 請畫圖描述 Multicast   ->->-> ``
<!--SR:!2023-12-11,155,230-->

#🧠 請畫圖描述 BroadCast  ->->-> ``
<!--SR:!2024-08-22,375,250-->

#🧠 請畫圖描述 UniCast  ->->-> ``
<!--SR:!2023-10-23,194,250-->


---
Status: #🌱 
Tags:
[[Network]]
Links:
[[分類定址是將IP分個群組來重新定義使用者能用的IP群組是什麼]]
References:
[[@dineshWhatUnicastBroadcast]]
[[@vivekreddyDifferenceUnicastBroadcast]]
