## 描述

[[@guptaStatelessnessRESTAPIs2018]]
> The application’s session state is therefore kept entirely on the client. The **client is responsible for storing and handling the session related information on its own** **side**.

> This also means that the client is responsible for sending any state information to the server whenever it is needed. There should not be any _**session affinity**_ or _**sticky session**_ between the client and the server.

> Statelessness means that every HTTP request happens in complete isolation. When the client makes an HTTP request, it includes all information necessary for the server to fulfill the request.
> 
> The server never relies on information from previous requests from the client. If any such information is important then the client will send that as part of the current request.


應用程式狀態完全由客戶端負責，換言之由客戶端負責儲存狀態、處理狀態相關的業務邏輯

statelessness 意思為 每個HTTP請求在狀態上都皆為獨立的，沒有一個請求是依賴前一個請求處理時會有的狀態資訊。 當客戶端發送請求，它會包含所有可以滿足伺服器處理需求的資料放在請求封包

這樣伺服器就不用依賴客戶端的前一個請求處理時的狀態。

[[@guptaStatelessnessRESTAPIs2018]]
> There are some very noticeable advantages of having **REST APIs stateless**.


> 1. Statelessness helps in scaling the APIs to millions of concurrent users by deploying it to multiple servers. Any server can handle any request because there is no session related dependency.


> 2. Being stateless makes REST APIs less complex – by removing all server-side state synchronization logic.
> 3. A stateless API is also easy to cache as well. Specific softwares can decide whether or not to cache the result of an HTTP request just by looking at that one request. There’s no nagging uncertainty that state from a previous request might affect the cacheability of this one. It improves the performance of applications.
>4. The server never loses track of “where” each client is in the application because the client sends all necessary information with each request.



[[@RestHowUnderstand]]
> Visibility is improved because a monitoring system does not have to look beyond a single request datum in order to determine the full nature of the request. Reliability is improved because it eases the task of recovering from partial failures. Scalability is improved because not having to store state between requests allows the server component to quickly free resources, and further simplifies implementation because the server doesn't have to manage resource usage across requests.

visibility 改善：
因為負責監聽執行情況的程式不必發送N個請求來完整理解1個會依賴這N個請求的處理狀態之請求。 造成這現象的原因會是指處理方本身不會依據狀態來處理

reliability 改善：
因為狀態處理全轉由客戶端來處理，處理方並不會處理，這使得處理方在獲得預期結果、承受故障、從故障恢復的能力提升

scalability 改善：
因為狀態處理全轉由客戶端來處理，處理方並不會處理，進而讓處理方不必考量狀態依賴問題來增加擴展的容易程度，比如處理方得考量擴展後的客戶端請求狀態要存在哪個主機、轉由哪個主機來處理等問題來擴展。


重點：
- stateful 是指特定系統或者特定程式會擁有狀態且會拿狀態進行處理
- statelessness 是指特定系統或者特定程式不會擁有任何狀態/擁有極少狀態且也不會依賴狀態來處理/極少機會會依賴狀態來處理。
	- 若API Server本身是statelessness或者stateless，會是指該API Server並不會儲存每次處理客戶端請求時的內容作為狀態並且也不會拿該狀態來處理客戶端的後續請求。
	- 若API Server本身是stateful，會是指該API Server會儲存每次處理客戶端請求的內容作為狀態並且拿狀態來處理客戶端的後續請求
- 客戶端和伺服器的狀態儲存/處理歸屬範圍：
- 
- API Server 不一定要滿足statelessness，主要要依據場景來調整
- 場景要求以下指標改善的話
	- Visibility
	- Reliability 
	- Scalability
- 若API Server是 statelessness或者stateless，那麼就能使以下指標得到改善：
	- visibility 改善： 因為負責監聽執行情況的程式不必發送N個請求來完整理解1個會依賴這N個請求的處理狀態之請求。 造成這現象的原因會是指處理方本身不會依據狀態來處理
	- reliability 改善：因為狀態處理全轉由客戶端來處理，處理方並不會處理，這使得處理方在獲得預期結果、承受故障、從故障恢復的能力提升
	- scalability 改善：因為狀態處理全轉由客戶端來處理，處理方並不會處理，進而讓處理方不必考量狀態依賴問題來增加擴展的容易程度，比如處理方得考量擴展後的客戶端請求狀態要存在哪個主機、轉由哪個主機來處理等問題來擴展。


## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References:
[[@RestHowUnderstand]]