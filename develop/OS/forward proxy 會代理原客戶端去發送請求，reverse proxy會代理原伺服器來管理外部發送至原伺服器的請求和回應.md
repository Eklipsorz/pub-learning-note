


## 描述
[[@wikidataProxyServer2022]] 所描述：
> In computer networking, a proxy server is a server application that acts as an intermediary between a client requesting a resource and the server providing that resource.
> 
![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Proxy_concept_en.svg/554px-Proxy_concept_en.svg.png)

[[@ReverseProxy2022]] 所描述：
> Reverse proxies are typically owned or managed by the web service, and they are accessed by clients from the public Internet. In contrast, a forward proxy is typically managed by a client (or their company) who is restricted to a private, internal network, except that the client can ask the forward proxy to retrieve resources from the public Internet on behalf of the client. 

[[@ask-xZhengXiangDaiLiFanXiangDaiLiBenZhiQuBie]] 所描述
> Unlike a [forward proxy](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Proxy_server%23Forward_proxy), which is an intermediary for its associated clients to contact any server, a reverse proxy is an intermediary for its associated servers to be contacted by any client。

> 翻译：正向代理是客户端和其他所有服务器（重点：所有）的代理者，而反向代理是客户端和所要代理的服务器之间的代理。

 

重點：
- proxy 是指代理人，某個人事A/主機A授與特定人事B/主機B一些使用權力來幫助人事A/主機A處理某事情，在這裡代理人會是指人事B/主機B
- 通常運用在電腦網路上的伺服器，一個專門被授與權力去幫忙特定主機做特定事情的伺服器，就叫代理伺服器，主要負責的任務內容會是依據委託方而定：
	- 假使是委託方是伺服器(在這裡並不是把代理伺服器視為伺服器)，那麼任務內容就有可能負責伺服器原本要做的事情
	- 假使是委託方是客戶端(在這裡並不是把代理伺服器視為伺服器下的客戶端)，那麼任務內容就有可能負責客戶端原本要做的事情
- 代理伺服器主要會根據客戶端A和伺服器B之間而區分兩種，在這裡的客戶端A是原本要向伺服器B發送請求，而伺服器B則是原本要替客戶端A進行回應的：
	- Forward Proxy
	- Reverse Proxy
	


### Forward Proxy 

1. 是指客戶端A授與權力給代理伺服器去幫忙做(客戶端A原本要做的事情-客戶端A向伺服器B發送回應)
2. 當客戶端A向伺服器B發送請求，會委託代理伺服器幫忙轉遞請求A，接著代理伺服器接收到請求A並轉遞至伺服器B進行處理，等到伺服器B處理完畢後，就將結果回傳給代理伺服器，最後代理伺服器收到回應後，並轉達回應給客戶端A
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656430766/blog/network/proxy/forward-proxy_sdzx6e.png)
	
### Reverse Proxy
1. 是指伺服器B授與權力請代理伺服器幫忙管理(伺服器B原本要做的事情-伺服器B接收客戶端A的請求並直接回應客戶端A的請求)外部主機發向伺服器B的請求和回應
2. 當外部主機(如客戶端A)向代理伺服器發送請求時，其代理伺服器就會將該請求導向至伺服器B，使伺服器B去處理，處理完畢後再由伺服器B將回應結果給代理伺服器，最後由代理伺服器把回應給外部主機(如客戶端A)
3. 另外也有可能會是：
	- 由伺服器管理員來建立其Reverse Proxy 架構，並讓伺服器B誤以為客戶端就只有Proxy Server，且伺服器B根本不知道真正的客戶端和自己之間是隔著Proxy Server
	- 伺服器B了解真正的客戶端和自己之間隔著Proxy Server
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656430766/blog/network/proxy/reverse-proxy_irssw8.png)
	
### Forward proxy 命名緣由
Forward 是指向前，Proxy是指代理人，合併起來就向前的代理人，在這裡會指著客戶端和伺服器之間的正常請求傳遞-客戶端請求伺服器：由客戶端請求proxy server幫忙做事情

### Reverse proxy 命名緣由
Reverse 是以什麼方向為主的逆方向Proxy是指代理人，合併起來就是以forward proxy為反轉方向的代理人，在這裡會指著客戶端和伺服器之間的反方向請求傳遞，也就是伺服器去請求proxy server幫忙做事情

### proxy 命名緣由
proxy: 
> the authority that you give to somebody to do something for you, when you cannot do it yourself

authority：
> the moral or legal right or ability to control
> 威信；權力；管轄權

重點：
- authority 是指合法權力、控制權
- proxy 是指代理人，也就是當你不能自己做某件事情A時，你授與權力給其他能做事情A的人
## 複習
#🧠 proxy 原意為何？(提示：你不能做的話，可不可找人做) ->->-> `proxy 是指代理人，也就是當你不能自己做某件事情A時，你授與權力給其他能做事情A的人 `
<!--SR:!2024-02-22,213,228-->

#🧠  authority 是指？ ->->-> `合法權力、控制權`
<!--SR:!2025-04-12,608,248-->

#🧠 proxy 套用在電腦主機的話，會是何種意思？ ->->-> `指代理人，某個人事A/主機A授與特定人事B/主機B一些使用權力來幫助人事A/主機A處理某事情，在這裡代理人會是指人事B/主機B`
<!--SR:!2024-08-25,479,250-->


#🧠 代理伺服器是什麼？做什麼？會不會任務有所變化，比如會變成客戶端或者伺服器？->->-> `通常運用在電腦網路上的伺服器，一個專門被授與權力去幫忙特定主機做特定事情的伺服器，就叫代理伺服器，主要負責的任務內容會是依據委託方而定 - 假使是委託方是伺服器(在這裡並不是把代理伺服器視為伺服器)，那麼任務內容就有可能負責伺服器原本要做的事情 - 假使是委託方是客戶端(在這裡並不是把代理伺服器視為伺服器下的客戶端)，那麼任務內容就有可能負責客戶端原本要做的事情`
<!--SR:!2024-01-07,129,228-->

#🧠 Forward proxy 命名緣由 ？ ->->-> `Forward 是指向前，Proxy是指代理人，合併起來就向前的代理人，在這裡會指著客戶端和伺服器之間的正常請求傳遞-客戶端請求伺服器：由客戶端請求proxy server幫忙做事情`
<!--SR:!2025-01-14,557,248-->

#🧠 Reverse proxy 命名緣由 ->->-> `Reverse 是以什麼方向為主的逆方向Proxy是指代理人，合併起來就是以forward proxy為反轉方向的代理人，在這裡會指著客戶端和伺服器之間的反方向請求傳遞，也就是伺服器去請求proxy server幫忙做事情`
<!--SR:!2025-01-01,548,248-->


#🧠 請用下圖來說明forward-proxy 在做什麼？(請務必說到客戶端A和伺服器B) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656430766/blog/network/proxy/forward-proxy_sdzx6e.png) ->->-> `1. 是指客戶端A授與權力給代理伺服器去幫忙做(客戶端A原本要做的事情-客戶端A向伺服器B發送回應) 2. 當客戶端A向伺服器B發送請求，會委託代理伺服器幫忙轉遞請求A，接著代理伺服器接收到請求A並轉遞至伺服器B進行處理，等到伺服器B處理完畢後，就將結果回傳給代理伺服器，最後代理伺服器收到回應後，並轉達回應給客戶端A`
<!--SR:!2024-07-12,453,250-->

#🧠 請用下圖來說明reverse-proxy 在做什麼？(請務必說到客戶端A和伺服器B)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656430766/blog/network/proxy/reverse-proxy_irssw8.png) ->->-> `當外部主機(如客戶端A)向代理伺服器發送請求時，其代理伺服器就會將該請求導向至伺服器B，使伺服器B去處理，處理完畢後再由伺服器B將回應結果給代理伺服器，最後由代理伺服器把回應給外部主機(如客戶端A)`
<!--SR:!2025-01-02,545,248-->

#🧠 代理伺服器會不會 "代理(動詞)" 伺服器 ？如果是的話，會做什麼？->->-> `是指伺服器B授與權力請代理伺服器幫忙管理(伺服器B原本要做的事情-伺服器B接收客戶端A的請求並直接回應客戶端A的請求)外部主機發向伺服器B的請求和回應`
<!--SR:!2025-01-05,548,248-->

#🧠 代理伺服器會不會代理客戶端？ 如果是的話，會做什麼？ ->->-> `是指客戶端A授與權力給代理伺服器去幫忙做(客戶端A原本要做的事情-客戶端A向伺服器B發送回應)`
<!--SR:!2024-09-02,485,250-->


#🧠 代理伺服器代理伺服器的話，外部客戶端A發過來的請求和伺服器B如何處理？ ->->-> `當外部主機(如客戶端A)向代理伺服器發送請求時，其代理伺服器就會將該請求導向至伺服器B，使伺服器B去處理，處理完畢後再由伺服器B將回應結果給代理伺服器，最後由代理伺服器把回應給外部主機(如客戶端A)`
<!--SR:!2024-09-11,489,250-->

#🧠 請問代理伺服器架構中，會不會有可能讓server認為proxy是它唯一的client端->->-> `有可能：- 由伺服器管理員來建立其Reverse Proxy 架構，並讓伺服器B誤以為客戶端就只有Proxy Server，且伺服器B根本不知道真正的客戶端和自己之間是隔著Proxy Server。 另一種可能- 伺服器B了解真正的客戶端和自己之間隔著Proxy Server`
<!--SR:!2024-03-25,223,190-->

---
Status: #🌱 
Tags:
[[Network]]
Links:
References:
[[@wikidataProxyServer2022]]
[[@ReverseProxy2022]]
[[@ask-xZhengXiangDaiLiFanXiangDaiLiBenZhiQuBie]]