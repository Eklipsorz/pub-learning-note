

## 描述
引用[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]所描述：
> region指資料中心的所在地，zone會是指實際資料中心

參考於[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]所描述
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653328292/blog/network/serverless/GCP-region_zone_zrcusp.png)

在這裡會有三個資料中心的所在地，分別有拉斯維加斯、東京、台灣彰化，每一個區域上皆會有三個資料中心(zone)所組成

每一個zone會是實際儲存實例(由軟體構建的執行環境、虛擬主機)，比如底下的虛擬主機就是儲存在東京地區的第二個zone
![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg)


## 複習

#🧠 GCP中的region和zone是指什麼？->->-> `region指資料中心的所在地，zone會是指實際資料中心`

#🧠 說明這張圖的region和zone再說明什麼，以GCP的region和zone概念來敘述 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653328292/blog/network/serverless/GCP-region_zone_zrcusp.png) ->->-> `在這裡會有三個資料中心的所在地，分別有拉斯維加斯、東京、台灣彰化，每一個區域上皆會有三個資料中心(zone)所組成`

#🧠 說明VM、Zone、Region的歸屬關係，是否為負責儲存VM? ![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg) ->->-> `每一個zone會是實際儲存實例(由軟體構建的執行環境、虛擬主機)，比如底下的虛擬主機就是儲存在東京地區的第二個zone`

---
Status: #🌱 
Tags: 
[[GCP]] - [[Serverless]]
Links:
References:
[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]