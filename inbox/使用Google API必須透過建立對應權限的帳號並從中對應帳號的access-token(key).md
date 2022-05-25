## 描述

若要在其他客戶端環境下來使用GCP SDK建立特定storage bucket以及在bucket建立物件的話，必須要先讓SDK能夠擁有足夠權限來調用對應API的資源，其方式主要有：
 - 使用對應權限的access-token

在這裡會探討著**使用對應權限的access-token**

流程有：
- 建立對應服務帳號
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653406080/blog/network/iam/create-service-account-first-step_epbv3e.png)
- 設定對應服務帳號所擁有的權限：在這裡會是Owner、Storage Admin、Storage Object Viewer、Storage Object Creator
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653406080/blog/network/iam/create-service-account-second-step_hfribp.png)
- 替對應服務帳號建立一組代表它權限的key或者access token
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653406552/blog/network/iam/create-access-token_cjyxma.png)
- 指定key格式為json，並下載至本地端存放
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653406552/blog/network/iam/access-token-type_nz2cnx.png)
- 設定環境變數GOOGLE_APPLICATION_CREDENTIAL，並指定為key目前所在
```
export GOOGLE_APPLICATION_CREDENTIAL=KEY_PATH
```

這樣就能讓SDK透過環境變數來讀取到key值，並確認它的權限是否能夠允許執行接下來使用者要求SDK要做的事情。

## 複習
#🧠 讓SDK能夠擁有足夠權限來調用對應API的資源，其方式主要有哪個方法？ ->->-> `使用對應權限的access-token`
<!--SR:!2022-05-28,3,250-->

---
Status: #🌱 
Tags: 
[[GCP]] - [[IAM]]
Links:
References:
[[@googlecloudCreateManageService]]
[[@eashish93BucketNameNeeded]]
