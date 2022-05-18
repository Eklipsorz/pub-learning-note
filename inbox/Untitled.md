
## 描述




### cast 含義
根據 [[@vivekreddyDifferenceUnicastBroadcast]]所描述的unicast、multicast、broadcast之間的差別：

> The **cast** term here signifies some data(stream of packets) is being transmitted to the recipient(s) from the client(s) side over the communication channel that helps them to communicate.

cast 指的是從(一個/多個)客戶端發送資料至(一個/多個)接收方 的行爲


### Unicast 
引用[[@dineshWhatUnicastBroadcast]]所描述的unicast定義


> Unicast is a type of communication where data is sent from one computer to another computer. In Unicast type of communication, there is only one sender, and one receiver.



> In computer networking, **unicast** is a one-to-one transmission from one point in the network to another point; that is, one sender and one receiver, each identified by a network address.

在電腦網路中，unicast 是指從一個主機A傳遞資訊至另一個主機B以及主機B接收自主機A傳遞過來的資訊

### Broadcast
> Broadcast is a type of communication where data is sent from one computer once and a copy of that data will be forwarded to all the devices.  

###  Multicast
> Multicast is a type of communication where multicast traffic addressed for a group of devices on the network. IP multicast traffic are sent to a group and only members of that group receive and/or process the Multicast traffic.


## 總結
引用[[@dineshWhatUnicastBroadcast]]: 
![[Pasted image 20220518202901.png]]


重點：
- unicast、broadcast、multicast 描述著一個綁定IP的主機發送封包的形式
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


---
Status: #📥 
Tags:
[[Network]]
Links:
References:
[[@dineshWhatUnicastBroadcast]]
[[@vivekreddyDifferenceUnicastBroadcast]]
