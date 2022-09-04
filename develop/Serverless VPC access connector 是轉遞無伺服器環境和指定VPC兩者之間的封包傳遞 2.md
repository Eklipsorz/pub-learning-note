
## 描述

### connector
連接器(Connector) 是 一種可以提供洞口來給予連接的裝置，並提供特定服務
> **a device that holds a wire in position in a piece of electrical equipment**


引用[[@googlecloudServerlessVPCAccess]]所描述的Serverless VPC access connector 意思：
> Serverless VPC Access makes it possible for you to connect directly to your Virtual Private Cloud network from serverless environments such as Cloud Run, App Engine, or Cloud Functions.
> Serverless VPC Access sends internal traffic from your VPC network to your serverless environment only when that traffic is a response to a request that was sent from your serverless environment through the Serverless VPC Access connector.

重點：
- Serverless VPC Access 背景是在 **Serverless Service本身只能對外開發，無法與VPC下的service進行連接，這使得部分服務無法間接提供給使用者**
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653397252/blog/network/serverless/serverless-service-network-when-built_gehol8.png)
- 為了解決第一點問題，就衍生Serverless VPC Access的概念，目的在於轉遞Serverless environment和VPC之間的封包轉遞，具體會使用connector來進行轉遞
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653398292/blog/network/serverless/serverless-service-network-to-connector_pb4710.png)
- 如上述，具體來說conenctor會被建立在VPC內部，由特定服務A所管理著，只要設定讓Serverless Service去指定使用哪一個connector，Serverless Service就能直接透過特定服務A來找到指定的connector來轉遞封包

- 當serviceless service向指定的connector轉發封包至VPC的Service，而connector收到後便以自己於VPC的IP轉遞封包給VPC下的Service，而Service收到就便處理，處理完畢後就將結果回傳至connector，麻煩轉遞至Serverless service，最後就從connector轉送至Serverless service，使它們收到


## 複習
#🧠 GCP - Serverless VPC access  背景是什麼 ->->-> `原本Serverless Service 是沒有與任何VPC進行連接，只能對外使用，但由於使用者若要索求VPC內的Service，則必須讓Serverless Server去連接VPC來獲取，所以就衍生出Serverless VPC access  `
<!--SR:!2022-09-22,76,250-->

#🧠 GCP - Serverless VPC access  是什麼樣的技術 ->->->  `具體透過access connector來轉遞VPC和Serverless environment兩者間的封包轉遞`
<!--SR:!2023-01-24,149,250-->

#🧠 Serverless VPC access connector 是什麼？->->-> `負責轉遞指定VPC和Serverless environment兩者間的封包轉遞`
<!--SR:!2022-09-11,69,250-->

#🧠 試說明一下VPC以外的App Engine傳遞請求封包至VPC的Service !![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653398292/blog/network/serverless/serverless-service-network-to-connector_pb4710.png)->->-> `在這裡App Engine為了傳送請求封包至VPC下的Service，而將封包轉遞給connector，由處於VPC的connector將封包傳給指定的VPC下Service，接著Service收到後就處理並向connector回傳結果，而connector就將結果轉遞至App Engine`
<!--SR:!2022-09-20,75,250-->

---
Status: #🌱 
Tags:
[[Network]] - [[Serverless]] - [[GCP]]
Links:
[[Serverless Computing 將對於伺服器本身的開發和管理 從開發抽離出來]]
[[設定Serverless VPC access connector 本身- 設定IP範圍、附加VPC、connector本身規格]]
[[VPC 如同實體網路可以擁有屬於自己的子網域]]
References:
[[@googlecloudServerlessVPCAccess]]