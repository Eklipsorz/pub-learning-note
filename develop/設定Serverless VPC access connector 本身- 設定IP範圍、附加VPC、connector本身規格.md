
## 描述

### 設定
connector 具體有幾項設定：
- Name: connector 本身名稱
- Region: connector 所處的區域是為何
- Network: connector 指定哪個VPC與連接器連接以及連接器處於哪個VPC
- Subnet: 設定VPC下的子網域來賦予connector來使用
- Scaling Settings: 設定當對於連接器的需求逐漸提高時，系統會動態調整連接器的數量好讓需求不被塞車問題給堵住，多出來的連接器同樣也會以名字為主
- Instance type: 設定擔任連接器的主機規格，規格越高，能接受的頻寬就越高

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653322301/blog/network/serverless/serverless-vpc-access-connector-setting-part1_dwqgsh.png)
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653323718/blog/network/serverless/serverless-vpc-access-connector-setting-part2_yf5aqq.png)

### 當設定完之後的情況
首先App Engine 、Cloud Functions、Cloud Run原本就是以提供外部存取的serverless service，所以會有外部IP，而在內部裡這些服務皆會包在某個特定VPC下的子網域，所以會有私人IP可以與GCP套件進行交流。

此外GCP內部網路中有數個VPC，而VPC又會像實體網路那樣，擁有子網域。

而當設定完connector，指定VPC網路會有一個connector，而他在VPC的網路IP會是
```
10.8.0.0/28
```
而當VPC外部的服務想要透過connector來轉發封包至內部的服務時，其實能透過serviceless VPC Access來找到對應的connector來進行轉發，這時connector就會透上述IP來轉發封包。
![](https://cloud.google.com/vpc/images/serverless-vpc-access.svg)


## 複習

#🧠 說明一下App Engine、Cloud Functions Cloud Run在GCP的網路狀況以及對外情形![](https://cloud.google.com/vpc/images/serverless-vpc-access.svg) ->->-> `App Engine 、Cloud Functions、Cloud Run原本就是以提供外部存取的serverless service，所以會有外部IP，而在內部裡這些服務皆會包在某個特定VPC下的子網域，所以會有私人IP可以與GCP套件進行交流。`
<!--SR:!2022-05-27,3,250-->

#🧠 說明一下當設定完時connector 的情況以及所處哪個網路？ ![](https://cloud.google.com/vpc/images/serverless-vpc-access.svg) ->->-> `當設定完connector，指定VPC網路會有一個connector，而他在VPC的網路IP會是10.8.0.0/28`
<!--SR:!2022-05-27,3,250-->

#🧠 說明一下connector 的情況，當外部網路想透過它轉發，會是？![](https://cloud.google.com/vpc/images/serverless-vpc-access.svg) ->->-> `當當VPC外部的服務想要透過connector來轉發封包至內部的服務時，其實能透過serviceless VPC Access來找到對應的connector來進行轉發，這時connector就會透上述IP來轉發封包`

---
Status: #🌱 
Tags:
[[Network]] - [[Serverless]] - [[GCP]]
Links:
[[GCP- region & zone，region 是指資料中心的所在地，泛指實際資料中心，zone會是指region的子區域，泛指實際資料中心的子資料中心]]
[[Serverless VPC access connector 是轉遞無伺服器環境和指定VPC兩者之間的封包傳遞]]
[[VPC 如同實體網路可以擁有屬於自己的子網域]]
References:
[[@googlecloudServerlessVPCAccess]]