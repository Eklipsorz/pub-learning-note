
## 描述

首先，express 伺服器會內建一個預設錯誤處理之middleware，在這裡基礎之下，只要App層級的middleware和Router層級的middleware遇到錯誤時，只要同個層級都沒專門處理錯誤的middleware，都會跑到預設錯誤處理之middleware進行處理
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png)

可若App層級就有預先自訂的middleware和Router層級就有預先自訂的middleware，其處理錯誤的流向會不同：
### 若App層級的middleware發生錯誤
當App層級的middleware發生錯誤時，會依序查看來執行：
- 是否有其他同層級的錯誤處理之middleware 1：在這裡假定是有的，那麼就會由它來處理錯誤，其next順序為如下，假如每個處理錯誤相關的middleware都有設定next的話，那麼順序會是：
	```
	app層級第一個先處理到的自製錯誤處理middleware -> 
	app層級第二個先處理到的自製錯誤處理middleware ->
	.
	.
	app層級最後一個先處理到的自製錯誤處理middleware ->
	預設錯誤處理之middleware
	```
	若中間沒next的話，就停留在沒next的錯誤處理middleware
	
- 跑到預設錯誤處理之middleware進行處理

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674927487/blog/middleware/error-handling/error-handling-in-app-adv_ceighd.png)






#### 若沒同層的錯誤處理middleware

但假如App層級沒有自製的錯誤處理middleware，那麼錯誤會轉移至Express預設的錯誤處理middleware
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-in-app-without-custom_xnq28p.png)

由於App層級**只會執行一個自製錯誤處理之middleware**，但沒有自製，只剩下只能直接預設錯誤處理middleware，所以沒next的必要

### 若Router層級的middleware發生錯誤
當App層級以middleware的形式來掛載Router層級的所有middleware，那麼Router層級middleware發生錯誤的話，會先依序查看來執行：
- 是否有同層級的錯誤處理middleware：假如有的話，就先執行同層級的middleware，其next順序如下，假如每個處理錯誤相關的middleware都有設定next的話，那麼順序會是：
	```
	Router 層級下的所有錯誤處理middleware(按出現順序) -> 
	接續Router之後的第一個app層級middleware ->
	預設錯誤處理之middleware
	```
	若中間沒next的話，就停留在沒next的錯誤處理middleware
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674926792/blog/middleware/error-handling/error-handling-in-route-adv_p3pa72.png)

- 自己被掛載到的層級是否有錯誤處理middleware：在這裡執行到這，就表示Router層級沒有專門處理錯誤的middleware，而轉由App層級的自製middleware執行，其next順序如下：
	```
	app層級第一個先處理到的自製錯誤處理middleware -> 預設錯誤處理之middleware
	```
	
	若中間沒next的話，就停留在沒next的錯誤處理middleware







#### 若沒同層級的錯誤處理middleware
在這裡執行到這，就表示Router層級沒有專門處理錯誤的middleware，而轉由App層級的自製middleware執行，其next順序如下：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656854628/blog/middleware/error-handling/error-handling-in-route-without-custom_wwsimj.png)



## 複習
#🧠 Express Server 提供哪幾種middleware來攔截錯誤並處理 (提示有三種) ->->-> `App層級的自製錯誤處理middleware、Router層級的自製錯誤處理middleware、Express 預設的錯誤處理middleware`
<!--SR:!2024-04-08,391,250-->

#🧠 假如Express Server上任何層級(App和Router)都沒有自製錯誤處理middleware，請問還會有誰能夠處理錯誤 ->->-> `Express 所預設的錯誤處理middleware`
<!--SR:!2023-10-16,283,250-->


#🧠 Express上若App 層級上的middleware出現錯誤時，其middleware會如何處理，假如其middleware架構會是如下圖(請考慮沒有自製和有自製的情形)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png)->->-> `首先若App層級的middleware出現錯誤時，會先查看App層級是否有自製的錯誤處理middleware，若有的話就執行那個；若沒有自製的錯誤處理middleware，會先執行Express 預設的錯誤處理middleware`
<!--SR:!2024-11-09,465,250-->


#🧠 Express上若App 層級上的middleware出現錯誤時，假如其middleware架構會是如下圖，在這裡若所有相關的錯誤處理middleware都有next，那麼會是什麼順序？(請考慮沒有自製和有自製的情形)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png) ->->-> `若有自製的app層級錯誤處理middleware，那麼當他執行next，只會告訴系統後續執行第二個層級，還有next一直到最後一個層級，都會使用app層級，直到最後app層級自製的middleware呼叫next才系統預設的錯誤處理middleware；若沒有自製的app層級錯誤處理middleware，那麼直接執行系統預設的錯誤處理middleware`
<!--SR:!2024-09-13,357,248-->






#🧠  Express上若App 層級上的middleware出現錯誤時，假如其middleware架構會是如下圖，在這裡若所有相關的錯誤處理middleware都有next，那麼假如app層級有7個自製的錯誤處理middleware，如何執行 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png) ->->-> `依序執行完所有middleware，然後藉由next()去執行系統預設的錯誤處理middleware`
<!--SR:!2024-07-30,392,250-->


#🧠 Express上若Router層級上的middleware出現錯誤時，假如其middleware架構會是如下圖，那麼其middleware會如何處理？(請考慮沒有自製和有自製的情形)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png) ->->-> `會先查看Router層級有沒有自製的錯誤處理middleware；若都沒有，就去查看App層級的自製錯誤處理middleware；再沒有的話，就直接執行系統預設的錯誤處理middleware`
<!--SR:!2023-10-19,200,230-->


#🧠 Express上router層級有許多自製的錯誤處理middleware，那麼假如Router層級的middleware發生錯誤，且每個相關的錯誤處理middleware都有呼叫next()，其順序會是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png) ->->-> `每個自製錯誤處理的middleware會先依出現順序來執行，最後自製的都處理完畢後，就接著執行接著router之後的app層級的所有自製錯誤處理系統預設的錯誤處理，接著才執行系統預測的錯誤處理middleware`
<!--SR:!2024-05-10,283,248-->




#🧠 Express上router層級沒有自製的錯誤處理middleware，那麼假如Router層級的middleware發生錯誤，且每個相關的錯誤處理middleware都有呼叫next()，其順序會是如何？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png) ->->-> `會先執行App層級的自製錯誤處理middleware，接著再執行系統預設的錯誤處理middleware`
<!--SR:!2024-05-08,281,230-->


---
Status: #🌱 
Tags:
[[Express]]
Links:
References:
