
## 描述

### connector
連接器(Connector) 是 一種可以提供洞口來給予連接的裝置，並提供特定服務
> **a device that holds a wire in position in a piece of electrical equipment**


引用[[@googlecloudServerlessVPCAccess]]所描述的Serverless VPC access connector 意思：
> Serverless VPC Access makes it possible for you to connect directly to your Virtual Private Cloud network from serverless environments such as Cloud Run, App Engine, or Cloud Functions.
> Serverless VPC Access sends internal traffic from your VPC network to your serverless environment only when that traffic is a response to a request that was sent from your serverless environment through the Serverless VPC Access connector.

重點：
- Serverless VPC Access 技術本身目的是允許Serverless Service能與特定VPC進行特定連接並相互傳遞訊息，Serverless Service能傳送/接收源自於VPC下的Service，而處於VPC下的Service能傳送/接受源自於VPC外部的Service


- 具體來說會使用一個轉接器或者連接器(connector)的實體物件來協助Serverless Server和VPC兩者間的資料傳遞，該連接器名為Serverless VPC access connector。

- 當建立好connector時，只要指定connectors哪一個VPC要被連接以及替Serverless Service指定哪一個connector進行連接，在這裡會是指定App Engine與connector進行連接，而附加至connector的VPC會是Virtual Private Cloud，這時只要VPC想向App Engine發送封包或者接收封包就只需透過Connector，反之；App Engine想向處於VPC 下的Server 發送封包或者接收封包，也只需要透過connector就能轉送
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653319253/blog/network/serverless/serverless-vpc-access-connector_myh7pz.png)

## 複習

#🧠 Serverless VPC access connector 是什麼？->->-> `負責轉遞指定VPC和Serverless environment兩者間的封包轉遞`
<!--SR:!2022-05-27,3,250-->

#🧠 試說明一下VPC下的server1和VPC以外的App Engine之間的連接情形 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653319253/blog/network/serverless/serverless-vpc-access-connector_myh7pz.png) ->->-> `只要指定connectors哪一個VPC要被連接以及替Serverless Service指定哪一個connector進行連接，在這裡會是指定App Engine與connector進行連接，而附加至connector的VPC會是Virtual Private Cloud，這時只要VPC想向App Engine發送封包或者接收封包就只需透過Connector，反之；App Engine想向處於VPC 下的Server 發送封包或者接收封包，也只需要透過connector就能轉送`

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