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


重點：
- API Server 不一定要滿足statelessness，依據場景來調整
- 若場景是要求提升
	- Visibility
	- Reliability 
	- Scalability


## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References:
[[@RestHowUnderstand]]