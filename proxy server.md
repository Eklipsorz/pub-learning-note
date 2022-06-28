


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
	- Forward Proxy ：是指客戶端A授與權力給代理伺服器去幫忙做(客戶端A原本要做的事情-客戶端A向伺服器B發送回應)客戶端A向伺服器B發送請求，在幫忙等待回應並讓伺服器B回應請求至代理伺服器，代理伺服器收到回應後，並轉達回應給客戶端A
	- Reverse Proxy：是指伺服器B授與權力請代理伺服器幫忙管理(伺服器B原本要做的事情-伺服器B接收客戶端A的請求並直接回應客戶端A的請求)外部主機發向伺服器B的請求和回應，當外部主機(如客戶端A)向代理伺服器發送請求時，其代理伺服器就會將該請求導向至伺服器B，使伺服器B去處理，處理完畢後再由伺服器B將回應結果給代理伺服器，最後由代理伺服器把回應給外部主機(如客戶端A)


### proxy 命名緣由
proxy: 
> the authority that you give to somebody to do something for you, when you cannot do it yourself

authority：
> the moral or legal right or ability to control
> 威信；權力；管轄權

重點：
- authority 是指合法全力、控制權
- proxy 是指代理人，也就是當你不能自己做某件事情A時，你授與權力給其他能做事情A的人
## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Network]]
Links:
References:
[[@wikidataProxyServer2022]]
[[@ReverseProxy2022]]
[[@ask-xZhengXiangDaiLiFanXiangDaiLiBenZhiQuBie]]