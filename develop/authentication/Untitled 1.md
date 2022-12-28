## 描述



### server-side session

> server-side session： the server generates and store some unique identifier
> store unique identifier on server, send some identifier to client


重點：
- server-side session：每到驗證成功就在server產生session並存放對應使用者資料、接著賦予session id給予客戶端，客戶端在請求封包裡夾雜session id，當伺服器要驗證id就會透過id去找尋對應session，進而獲取進一步的資料和驗證。
-  帶來的好處就是：
	- 相較於使用固定字串來做為access來說，較不容易偽造其access
- 帶來的壞處就是：
	- 需要伺服器額外處理空間成本和時間成本在session的儲存、管理、獲取、驗證上
	- Monitoring System上的Visibility、Reliability、Scalability會不容易提升。
[[API Server 不一定要滿足statelessness，主要要依據場景來調整，場景為需要改善- Visibility - Reliability  - Scalability 等指標的場景]]



## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[API Server 不一定要滿足statelessness，主要要依據場景來調整，場景為需要改善- Visibility - Reliability  - Scalability 等指標的場景]]
[[在電腦科學中，scalability 是指當為了讓應用程式更能滿足需求而擴展硬體效能或者其他效能的情況下，特定電腦程式還能夠繼續正常執行的程度]]
[[Reliability 泛指著使用者對於特定軟體執行出預期結果所能信賴的程度，具體為在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度]]
[[在電腦科學中的monitoring tool 中，visibility 是指特定監測結果可被看見的程度，或者特定監測結果可見到的容易程度]]
References: