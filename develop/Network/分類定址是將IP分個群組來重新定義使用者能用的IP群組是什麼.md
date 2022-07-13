## 描述


分類定址原文為 **Classful Addressing**，被提出的背景是出自於：
- 原本是以32位元中的8位元來定義子網域，其中24位元是定義在子網域下的獨特序號
- 造成問題主要有二個：區域網域的盛行導致目前定義的子網域無法滿足、一個網域分配的IP遠超於業界所需
- 剩下可參考於[[網路IP的子網域是從8位元演變至classful addressing]]

### 分類定址
是將IP分成五大種類的IP，並給予每個種類不同的設定，讓需求方能夠根據設定來選擇，並且加以管理每個網域和網域下的每個IP
	- 網路下的所有主機之間的傳播模式是什麼(unicast / multicast)
	- 多少個子網域、每一個子網路能夠分到多少


### IP結構
IP由Network ID、Host ID所構成，而Network ID最前面幾位元會是代表該IP是屬於哪一類：
- Class A：IP上起始位(第一個bit)是0
- Class B：IP上起始前兩位是10
- Class C：IP上起始前三位是110
- Class D：IP上起始前四位是1110
- Class E：IP上起始前五位是11110

而剩下的Network ID的辨識則是用網路遮罩[[網路遮罩是用來判斷目前IP所屬的子網域是什麼]]的技術來區分不同種類下的不同子網域

引用於[[@lokeshgallaIPv4ClassesRanges]]所提供的圖：
![](https://www.researchgate.net/profile/Lokesh-Galla/publication/260622269/figure/fig1/AS:340713477820416@1458243831010/1-1-IPv4-Classes-Ranges.png)


### Class A
Class A 的IP範圍和遮罩分別為：
- IP: 0.0.0.0 ~ 127.255.255.255
- Mask: 255.0.0.0
- 具體能分到的子網路數是128個(0-127)
- 具體每個子網路能分到IP的總主機數為$2^{24}-2$個主機，扣2是指扣掉識別用的IP和廣播用的IP[[一個IP群組上一定會有負責用來識別整個IP群組以及廣播位址]]
- 傳播模式：單播

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1652890427/obsidian/network/classA-IP_ose9qj.png)
### Class B

Class B 的IP範圍和遮罩分別為：
- IP: 128.0.0.0 ~ 191.255.255.255
- Mask: 255.255.0.0
- 具體能分到的子網路數是$64*256 = 16384$個
- 具體每個子網路能分到IP的總主機數為$2^{16}-2$個主機
- 傳播模式：單播

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1652890427/obsidian/network/classB-IP_anrihm.png)

### Class C
Class C的IP範圍和遮罩分別為：
- IP: 192.0.0.0~223.255.255.255
- Mask: 255.255.255.0
- 具體能分到的子網路數是$32*256*256 = 2097152$個
- 具體每個子網路能分到IP的總主機數為$256-2=254$個主機
- 傳播模式：單播

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1652890427/obsidian/network/classC-IP_dedinz.png)
### Class D
Class D的IP範圍和遮罩分別為：
- 224.0.0.0~239.255.255.255
- Mask： 255.255.255.255
- 具體能分到的子網路數是 $2^{28} = 268435456$個
- 具體每個子網路能分到IP的總主機數為 $0$個主機
- 傳播模式：多播 or 廣播

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1652890427/obsidian/network/classD-IP_bamrv4.png)

## 複習
#🧠 分類定址的提出主因為 ->->-> `由於區域網域的盛行而導致那時定義的256個子網域不太能滿足需求 和 一個子網域分配的IP遠超於需求`
<!--SR:!2022-08-29,63,250-->

#🧠 分類定址(Classful Addressing) 具體用途是什麼？如何做？ ->->-> `用途為劃分IP為五個設定不同的IP類別並加以方便選擇使用和管理，每個設定具體定義子網域數量、每個子網域的總IP數、傳播是否單播或者多播，具體作法會是使用網路遮罩的技術初步將IP分為三類的IP群組`
<!--SR:!2022-07-27,39,230-->

#🧠 Classful addressing: 各類的Class IP範圍和遮罩各為多少 ->->-> `class A的IP範圍為0.0.0.0~127.255.255.0，class B的IP範圍為128.0.0.0~191.255.255.255，class C的IP範圍為192.0.0.0~223.255.255.255，遮罩分別為255.0.0.0、255.255.0.0、255.255.255.0`
<!--SR:!2022-10-14,93,250-->




---
Status: #🌱 
Tags:
[[Network]]
Links:
[[網路IP的子網域是從8位元演變至classful addressing]]
[[網路遮罩是用來判斷目前IP所屬的子網域是什麼]]
[[一個IP群組上一定會有負責用來識別整個IP群組以及廣播位址]]
References:
[[@wikidataZiWangYu2021]]
[[@lokeshgallaIPv4ClassesRanges]]