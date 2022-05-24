

## 描述

引用[[@wikidataServerlessComputing2022]]所述的Serverless Computing 定義：
> **Serverless computing** is a cloud computing execution model in which the cloud provider allocates machine resources on demand, taking care of the servers on behalf of their customers. "Serverless" is a misnomer in the sense that servers are still used by cloud service providers to execute code for developers. However, developers of serverless applications are not concerned with capacity planning, configuration, management, maintenance, fault tolerance, or scaling of containers, VMs, or physical servers. Serverless computing does not hold resources in volatile memory; computing is rather done in short bursts with the results persisted to storage. When an app is not in use, there are no computing resources allocated to the app. Pricing is based on the actual amount of resources consumed by an application.[1] It can be a form of utility computing.


引用[[@cloudflareShiMoShiWuSiFuQiJiSuanWuSiFuQiDingYi]]所述的Serverless Computing 定義：
> 無伺服器計算是一種按需提供後端服務的方法。無伺服器提供者允許用戶編寫和部署代碼，而不必擔心底層基礎結構。從無伺服器提供商獲得後端服務的公司將根據計算量來付費，由於這種服務是自動擴展的，不必預留和付費購買固定數量的頻寬或伺服器。請注意，雖然名為「無伺服器」，實際上依然需要物理伺服器，只不過開發人員不需要考慮伺服器而已。

重點：
- Serverless computing 中的serverless是指對於面向於computing的使用者(開發人員)來說，使用者在使用上不必考慮伺服器本身所需的開發和維護並為此親自實現，只需要考慮如何開發開發項目本身，所以使用者來說，等同於無伺服器為主的開發。
- 面向於computing的提供者來說，是要替使用者處理伺服器本身所需要做的開發、設定、維護，所以對於提供者，不完全是無伺服器為主。
- serverless computing 真正描述是以使用者的角度來說，而非是提供者。
- 第一張為nonserverless environment，提供者會負責處理使用者主機所在的環境是否穩定，使用者負責處理提供者所給予的主機(Host)環境以及如何在主機環境進行開發
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653314112/blog/network/serverless/non-serverless-env_bbi9ve.png)
第二張為serverless environment，提供者會負責使用者主機所在的環境是否穩定以及負責原本執行開發項目的主機，使用者只需要負責開發項目的開發，並且將項目部署至開發者指定的主機上
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653314112/blog/network/serverless/serverless-env_a6j5mv.png)
- 由於前述描述，提供者可以將服務調節成按照App所需來調整執行App的環境是如何。


### 案例
Serverless service:
- Cloud Run
- App Engine
- Cloud Function
- Heroku
- Firebase

## 複習

#🧠 無伺服器計算的命名緣由 ->->-> `serverless computing 真正描述是以使用者的角度來說，而非是提供者，所以對於使用者來說，不必考慮伺服器本身所需的開發和維護並為此親自實現，只需要考慮如何開發開發項目本身，所以使用者來說，等同於無伺服器為主的開發，而提供者會是要替使用者處理伺服器本身所需要做的開發、設定、維護`
<!--SR:!2022-05-25,1,230-->

#🧠 這圖說明nonserverless environment，請解釋Provider和User負責了什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653314112/blog/network/serverless/non-serverless-env_bbi9ve.png) ->->-> `提供者會負責處理使用者主機所在的環境是否穩定，使用者負責處理提供者所給予的主機(Host)環境以及如何在主機環境進行開發`
<!--SR:!2022-05-26,2,248-->

#🧠 這圖說明serverless environment，請解釋Provider和User負責了什麼？  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653314112/blog/network/serverless/serverless-env_a6j5mv.png) ->->-> `提供者會負責使用者主機所在的環境是否穩定以及負責原本執行開發項目的主機，使用者只需要負責開發項目的開發，並且將項目部署至開發者指定的主機上`
<!--SR:!2022-05-27,3,250-->

---
Status: #🌱 
Tags:
[[Network]] - [[Serverless]]
Links:
[[虛擬雲 或 虛擬網路 是以軟體形式來實現組成網路所需的儀器以及機制，從而組成虛擬網路]]
[[GCP serverless service 在一開始被建立後所處的網路能夠對外，但不是處於VPC]]
References:
[[@wikidataServerlessComputing2022]]
[[@cloudflareShiMoShiWuSiFuQiJiSuanWuSiFuQiDingYi]]