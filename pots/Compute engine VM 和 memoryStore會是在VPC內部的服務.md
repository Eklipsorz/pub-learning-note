
## 描述

引用[[@googlecloudServerlessVPCAccess]]所描述的VPC內部服務：
> This page shows how to use [Serverless VPC Access](https://cloud.google.com/vpc/docs/serverless-vpc-access) to connect your serverless environment directly to your VPC network, allowing access to Compute Engine VM instances, Memorystore instances, and any other resources with an internal IP address.

重點：
- serverless environment 本身不是處於VPC
- Compute Engine VM instance 、MemoryStore instance、其他擁有內部IP的資源(如serverless access connector)



## 複習
#🧠 serverless environment 、 compute engine vm instance、memorystore instance哪一個處於VPC的服務? 哪一個不處於VPC的服務->->-> `serverless environment 本身不是處於VPC，Compute Engine VM instance 、MemoryStore instance、其他擁有內部IP的資源(如serverless access connector)則是處於VPC下的服務`
<!--SR:!2022-05-27,3,250-->


---
Status: #🌱 
Tags:
[[GCP]] - [[VPC]]
Links:
References:
[[@googlecloudServerlessVPCAccess]]