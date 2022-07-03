
## 描述

首先，express 伺服器會內建一個預設錯誤處理之middleware，在這裡基礎之下，只要App層級的middleware和Router層級的middleware遇到錯誤時，只要同個層級都沒專門處理錯誤的middleware，都會跑到預設錯誤處理之middleware進行處理
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-sample_nv3br8.png)

可若App層級就有預先自訂的middleware和Router層級就有預先自訂的middleware，其處理錯誤的流向會不同：
### 若App層級的middleware發生錯誤
當App層級的middleware發生錯誤時，會查看是否有其他同層級的錯誤處理之middleware A，在這裡假定是有的，那麼就會由它來處理錯誤，若該錯誤處理middleware A有呼叫next()，那麼就在該middleware 執行完畢後會執行系統預設錯誤處理之middleware；
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-in-app_cse9b3.png)

反之若沒呼叫next的話，就會停在middleware A，不繼續處理錯誤。

但假如App層級沒有自製的錯誤處理middleware，那麼錯誤會轉移至Express預設的錯誤處理middleware
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656852567/blog/middleware/error-handling/error-handling-in-app-without-custom_xnq28p.png)

### 若Router層級的middleware發生錯誤
當App層級以middleware的形式來掛載Router層級的所有middleware，那麼Router層級middleware發生錯誤的話，會先查看以下幾點：
	- 是否有同層級的錯誤處理middleware：若有的話，就執行該middleware，但若繼續執行next()，會直接跳至預設的錯誤處理middleware，沒有的話就按下一個選項來找middleware來處理
	- 自己被掛載到的層級是否有錯誤處理middleware：
	- 都
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656851609/blog/middleware/error-handling/error-handling-in-route_klvzoa.png)

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
