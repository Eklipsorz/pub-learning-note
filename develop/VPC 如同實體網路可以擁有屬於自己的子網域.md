
## 描述

引用[[@googlecloudVPCNetworkOverviewa]]所描述的圖：
![](https://cloud.google.com/vpc/images/vpc-overview-example.svg?hl=de)

以及引用[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]所描述的
![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg)


重點：
- 一個VPC本身會如同一個實體網路那樣，擁有多個子網域(subnet)來分配
- 每一個子網域可以被分配至每一個區域(region)，每個區域可以擁有一個以上的子網域
- 當區域被分配子網域時，該區域下的所有zone將會根據子網域規定的IP範圍來實際定義資料中心下所建立的實例所擁有的IP，如嘉義地區被分配到192.168.0.0/24這IP，那麼其嘉義地區所建立的虛擬機內部IP會是由該192.168.0.0/24來決定


### 案例1
以第一張為例，VPC擁有三個子網域分別為如下，而第一個子網域分配給us-west1這區域，第二～三個子網域分配給us-east1這區域
```
10.240.0.0/24
192.168.1.0/24
10.2.0.0/16
```
![](https://cloud.google.com/vpc/images/vpc-overview-example.svg?hl=de)

接著us-west1下有二台虛擬機，實際下會是在us-west-a所建立的，而它的內部IP分配會是
```
10.240.0.0/24
```

緊接著，us-east1下有二台虛擬在192.168.1.0/24這個子網域，而另外兩台在10.2.0.0/16這個子網域，其中在192.168.1.0/24子網域的兩台虛擬機皆在us-east1-a所建立，而另外兩台則是一個是在us-east1-a這資料中心所建立，另一個則是在us-east-b這資料中心所建立


### 案例2

在這裡VPC有三個子網域，前面兩個子網域分配給東京地區，東京地區的所有資料中心下所建立的實例可從這兩個子網域來分配IP，VPC下的最後子網域則是分給嘉義地區，嘉義地區的所有資料中心下所建立的實例可從最後一個子網域來分配IP

![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg)
## 複習
#🧠 VPC、子網域、區域的關係會是如何？->->-> `一個VPC本身會如同一個實體網路那樣，擁有多個子網域(subnet)、每一個子網域可以被分配至每一個區域(region)，每個區域可以擁有一個以上的子網域、當區域被分配子網域時，該區域下的所有zone將會根據子網域規定的IP範圍來實際定義資料中心下的實例所擁有的IP`

#🧠 說明VPC和子網域的關係、子網域下實際分配給哪些地區、地區又是如何分配IP? ![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg) ->->-> `在這裡VPC有三個子網域，前面兩個子網域分配給東京地區，東京地區的所有資料中心下所建立的實例可從這兩個子網域來分配IP，VPC下的最後子網域則是分給嘉義地區，嘉義地區的所有資料中心下所建立的實例可從最後一個子網域來分配IP`
<!--SR:!2022-05-27,3,250-->



---
Status: #🌱 
Tags:
[[Network]] - [[VPC]] - [[GCP]]
Links:
[[GCP- region & zone，region 是指資料中心的所在地，泛指實際資料中心，zone會是指region的子區域，泛指實際資料中心的子資料中心]]
[[Serverless VPC access connector 是轉遞無伺服器環境和指定VPC兩者之間的封包傳遞]]
[[設定Serverless VPC access connector 本身- 設定IP範圍、附加VPC、connector本身規格]]
References:
[[@googlecloudVPCNetworkOverviewa]]
[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]