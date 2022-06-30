
## 描述
一個IP群組上一定會有兩個IP是由於用途關係而無法直接分配給主機：
- 識別用的IP
- 廣播用的IP



### 識別用的IP
用來識別IP所屬子網域的序號，通常會拿子網域的第一個IP來當作識別這子網域的識別碼

假如說的IP範圍是128.0.0.0 ~ 128.0.0.25，那麼若要將這範圍內的IP視為一個子網域，就會拿第一個IP當作識別用這個子網域的IP


### 廣播用的IP
根據[[@wikidataBroadcastAddress2022]]所提到的，這IP是負責轉達訊息至所屬網域下的所有IP，只要有人傳遞訊息至該廣播用的IP，就會立即轉達訊息至所有IP

> A **broadcast address** is a network address used to transmit to all devices connected to a multiple-access communications network. A message sent to a broadcast address may be received by all network-attached hosts.

### 以0或255結尾的位址誤解
[[以0或255結尾的位址不一定是識別用和廣播用的]]


## 複習
#🧠 IP群組上一定會有兩個IP是由於用途關係而無法直接分配給主機，具體是什麼 ->->-> `識別網域用的IP、廣播用的IP`
<!--SR:!2022-09-06,68,250-->

#🧠 識別網域用的IP是做什麼，具體會用什麼序號當做其IP->->-> `用來識別IP所屬子網域的序號，通常會拿子網域的第一個IP來當作識別這子網域的識別碼`
<!--SR:!2022-07-10,34,250-->

#🧠 廣播用的IP是做什麼？廣播又是什麼 ->->-> `這IP是負責轉達訊息至所屬網域下的所有IP，只要有人傳遞訊息至該廣播用的IP，就會立即轉達訊息至所有IP`
<!--SR:!2022-07-05,31,250-->


---
Status: #🌱 
Tags:
[[Network]]
Links:
[[以0或255結尾的位址不一定是識別用和廣播用的]]
References:
[[@wikidataIPv42022]]
[[@wikidataBroadcastAddress2022]]