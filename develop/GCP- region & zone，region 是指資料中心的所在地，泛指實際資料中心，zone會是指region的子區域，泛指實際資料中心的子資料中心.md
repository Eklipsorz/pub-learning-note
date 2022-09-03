

## 總結
- GCP的資源會是由數個坐落於世界各地的實體資料中心
- 每個實體資料中心會以region來表示和用region表示其資料中心的實際所在
- 每個實體資料中心可以進一步(邏輯上切分)切分數個子資料中心來儲存資料，這些子資料中心會由zone來表示，且region和zone之間關係會是 **zone會是region下的子區域**

## 描述
引用[[@googlecloudRegionsZonesCompute]]所述
> Compute Engine resources are hosted in multiple locations worldwide. These locations are composed of regions and zones. A region is a specific geographical location where you can host your resources. Regions have three or more zones. For example, the `us-west1` region denotes a region on the west coast of the United States that has three zones: `us-west1-a`, `us-west1-b`, and `us-west1-c`.

> Resources that live in a zone, such as [virtual machine instances](https://cloud.google.com/compute/docs/instances) or zonal [persistent disks](https://cloud.google.com/compute/docs/disks), are referred to as zonal resources. Other resources, like [static external IP addresses](https://cloud.google.com/compute/docs/ip-addresses#reservedaddress), are regional

重點：
- GCP的資源會作落於世界各地的資料中心，而每個資料中心會由數個region和數個zone所組成
- 一個region會是指實際資料中心的所在地，或者是存放資源的所在地，而一個region可被切分數個zone


引用[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]所描述：
> region指實際資料中心的所在地，泛指著那個地區下的資料中心，zone會是指region下的子區域，泛指著那個實際資料中心切分出來的邏輯(logical)/虛擬(virtual)資料中心，或者說是從實際資料中心切分出來的子資料中心，只是以軟體形式來切分出來

參考於[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]所描述
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653328292/blog/network/serverless/GCP-region_zone_zrcusp.png)

在這裡會有三個資料中心的所在地，分別有拉斯維加斯、東京、台灣彰化，每一個區域上皆會有三個資料中心(zone)所組成

每一個zone會是實際儲存實例(由軟體構建的執行環境、虛擬主機)，比如底下的虛擬主機就是儲存在東京地區的第二個zone
![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg)


## 複習

#🧠 GCP中的region和zone是指什麼？->->-> `region 是指資料中心的所在地，泛指實際資料中心，zone會是指region的子區域，泛指實際資料中心的子資料中心`
<!--SR:!2022-09-26,79,250-->

#🧠 說明這張圖的region和zone再說明什麼，以GCP的region和zone概念來敘述 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653328292/blog/network/serverless/GCP-region_zone_zrcusp.png) ->->-> `在這裡會有三個資料中心的所在地，分別有拉斯維加斯、東京、台灣彰化，每一個區域上皆會有三個子資料中心(zone)所組成`
<!--SR:!2022-10-30,76,230-->

#🧠 說明VM歸屬於誰？為什麼? ![](https://i.ytimg.com/vi/yygf4MOmI-E/maxresdefault.jpg) ->->-> `每一個zone會是實際儲存實例(由軟體構建的執行環境、虛擬主機)，比如底下的虛擬主機就是儲存在東京地區的第二個zone`
<!--SR:!2023-02-10,160,250-->

---
Status: #🌱 
Tags: 
[[GCP]] - [[Serverless]]
Links:
References:
[[@samtsaiGCPTuJieJiaoXueNetworkVPCSubnet]]
[[@googlecloudRegionsZonesCompute]]