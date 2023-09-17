## 描述



### server-side session

> server-side session： the server generates and store some unique identifier
> store unique identifier on server, send some identifier to client


重點：
- server-side session 隸屬於session-based authentication
- server-side session：伺服器會替客戶端請求的處理內容儲存，以session形式來儲存在session store並產生獨特識別碼來對應其session，接著賦予識別碼給予客戶端，以便下一次連接互動時，可繼續以上一個請求的處理內容來處理接下來的請求處理
- 應用：
	- 登入驗證
-  以server-side session為基礎的應用所帶來的好處就是：
	- 相較於使用固定字串來做為access來說，較不容易偽造其代表access的識別字，因為可以在伺服器內使用亂數來產生，外部的人並不會知道
- 以server-side session為基礎的應用所帶來的壞處就是：
	- 需要伺服器額外處理空間成本和時間成本在session的儲存、管理、獲取、驗證上
	- Monitoring System上的Visibility、Reliability、Scalability會不容易提升。
[[API Server 不一定要滿足statelessness，主要要依據場景來調整，場景為需要改善- Visibility - Reliability  - Scalability 等指標的場景]]


### 登入驗證：獲取對應permission 或者 access的 流程

1. 客戶端先輸入自己的credential並傳遞給伺服器做驗證
2. 伺服器收到就從資料庫獲取對應使用者的credential來比對輸入的credential是否一樣，若一樣就做下一步；若不一樣就報錯
3. 伺服器建立session 來儲存credential並將該session儲存至伺服器上的session store
4. 伺服器在回傳session id給客戶端，作為代表permission或者access，
5. 此時客戶端收到會存放在自己的cookie並標記對應domain和path來表示這資料屬於哪個domain和path。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1672251336/blog/authentication/server-side-authentication-session-generate_wmtpwy.png)



### 登入驗證：利用permission 或者access來索要受保護的資源之流程

1. 客戶端發送請求時，會根據請求端點和伺服器來從客戶端的cookie找到相對應的資料夾雜在請求封包內，在這裡會是session id
2. 伺服器收到請求時，就會拿session id去從對應session store找到對應的session，若找到就得到對應的credential；若找不到就報錯
3. 伺服器就將請求回應傳送給客戶端

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1672251336/blog/authentication/server-side-authentication-session-compare_g9vnft.png)



## 複習

#🧠 server-side session 是什麼樣的技術 ->->-> `伺服器會替客戶端請求的處理內容儲存，以session形式來儲存在session store並產生獨特識別碼來對應其session，接著賦予識別碼給予客戶端，以便下一次連接互動時，可繼續以上一個請求的處理內容來處理接下來的請求處理`
<!--SR:!2024-06-26,329,250-->

#🧠  server-side session 可應用什麼服務？->->-> `登入驗證`
<!--SR:!2023-10-12,112,230-->

#🧠 以server-side session為基礎的應用所帶來的好處就是？ ->->-> `可依據先前與客戶端之間的狀態進行更進階的處理、相較於使用固定字串來做為access來說，較不容易偽造其代表access的識別字，因為可以在伺服器內使用亂數來產生，外部的人並不會知道`
<!--SR:!2023-11-28,204,250-->


#🧠 以server-side session為基礎的應用所帶來的好處就是？(狀態依賴、偽造) ->->-> `可依據先前與客戶端之間的狀態進行更進階的處理、相較於使用固定字串來做為access來說，較不容易偽造其代表access的識別字，因為可以在伺服器內使用亂數來產生，外部的人並不會知道`
<!--SR:!2023-11-25,95,230-->

#🧠 以server-side session為基礎的應用所帶來的好處就是？->->-> `可依據先前與客戶端之間的狀態進行更進階的處理、相較於使用固定字串來做為access來說，較不容易偽造其代表access的識別字，因為可以在伺服器內使用亂數來產生，外部的人並不會知道`
<!--SR:!2023-11-24,94,230-->


#🧠 以server-side session為基礎的應用所帶來的好處為何就是較不容易偽造其代表access的識別字 ->->-> `因為可以在伺服器內使用亂數來產生，外部的人並不會知道`
<!--SR:!2024-06-29,332,250-->

#🧠 以server-side session為基礎的應用所帶來的壞處就是？（提示：有兩大點） ->->-> `需要伺服器額外處理空間成本和時間成本在session的儲存、管理、獲取、驗證上、Monitoring System上的Visibility、Reliability、Scalability會不容易提升`
<!--SR:!2023-10-28,46,227-->


#🧠 以server-side session為基礎的應用所帶來的壞處就是？ ->->-> `需要伺服器額外處理空間成本和時間成本在session的儲存、管理、獲取、驗證上、Monitoring System上的Visibility、Reliability、Scalability會不容易提升`
<!--SR:!2023-11-19,63,247-->



#🧠 以server-side session為基礎來構建登入驗證服務：獲取對應permission 或者 access的 流程，請問流程會是什麼？ ->->-> `1. 客戶端先輸入自己的credential並傳遞給伺服器做驗證 2. 伺服器收到就從資料庫獲取對應使用者的credential來比對輸入的credential是否一樣，若一樣就做下一步；若不一樣就報錯 3. 伺服器建立session 來儲存credential並將該session儲存至伺服器上的session store 4. 伺服器在回傳session id給客戶端，作為代表permission或者access， 5. 此時客戶端收到會存放在自己的cookie並標記對應domain和path來表示這資料屬於哪個domain和path。`
<!--SR:!2024-06-18,323,250-->

#🧠 以server-side session為基礎來構建登入驗證服務：獲取對應permission 或者 access的 流程，請問流程會是什麼？以畫圖表示->->-> ``
<!--SR:!2024-04-27,291,250-->


#🧠 以server-side session為基礎來構建登入驗證服務：利用permission 或者access來索要受保護的資源之流程是什麼？ ->->-> `1. 客戶端發送請求時，會根據請求端點和伺服器來從客戶端的cookie找到相對應的資料夾雜在請求封包內，在這裡會是session id 2. 伺服器收到請求時，就會拿session id去從對應session store找到對應的session，若找到就得到對應的credential；若找不到就報錯 3. 伺服器就將請求回應傳送給客戶端`
<!--SR:!2024-06-27,330,250-->
#🧠 以server-side session為基礎來構建登入驗證服務：利用permission 或者access來索要受保護的資源之流程，請問流程會是什麼？以畫圖表示->->-> ``
<!--SR:!2024-06-28,331,250-->


#🧠 server-side session作為登入驗證方法，請問它隸屬於哪一種類的技術? 是屬於token based? 還是session based? ->->-> `session based authentication`
<!--SR:!2023-11-10,122,250-->

---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[API Server 不一定要滿足statelessness，主要要依據場景來調整，場景為需要改善- Visibility - Reliability  - Scalability 等指標的場景]]
[[在電腦科學中，scalability 是指當為了讓應用程式更能滿足需求而擴展硬體效能或者其他效能的情況下，特定電腦程式還能夠繼續正常執行的程度]]
[[Reliability 泛指著使用者對於特定軟體執行出預期結果所能信賴的程度，具體為在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度]]
[[在電腦科學中的monitoring tool 中，visibility 是指特定監測結果可被看見的程度，或者特定監測結果可見到的容易程度]]
[[登入驗證概念為透過與伺服器間的credential驗證過程來獲取access並利用access來向伺服器索求受保護的資源]]
References: