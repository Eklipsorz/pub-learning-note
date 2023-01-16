## 描述

### Context 侷限問題


> React Context is specifically not optimized for high frequency changes
> for example, if you have state changes every second or multiple times per second

> React Context also shouldn't be used to replaced all component communications and props


> component should still be configurable via props and short "props chains" might not need any replacement

[[@sebmarkbageProvideMoreWays]]
> My personal summary is that new context is ready to be used for low frequency unlikely updates (like locale/theme). It's also good to use it in the same way as old context was used. I.e. for static values and then propagate updates through subscriptions. It's not ready to be used as a replacement for all Flux-like state propagation.


重點：
- React Context 本身並沒有針對狀態的高頻率變動做出較為優化的實現，目前停留在適用於狀態變動頻率較低的場景下：
	- 高頻率變動：每秒有多個狀態改變
- Context 使用提醒：
	- props 是用來製作可重複使用元件的手段，Context 只是負責作多個元件之間的狀態傳遞
	- 不應該全面取代所有元件的狀態傳輸和props
	- 若元件本身是用props來建構 或者使用較短的props chains 可以不需要用Context來替代



## 複習

#🧠 React Context 侷限是什麼？ ->->-> `本身並沒有針對狀態的高頻率變動做出較為優化的實現，目前停留在適用於狀態變動頻率較低的場景下`
<!--SR:!2023-06-17,163,250-->

#🧠 React Context 侷限是本身並沒有針對狀態的高頻率變動做出較為優化的實現，其中高頻率是指？ ->->-> `每秒有多個狀態改變`
<!--SR:!2023-07-29,194,250-->

#🧠 React Context 和 React Props之間的差異？ ->->-> `props 是用來製作可重複使用元件的手段，Context 只是負責作多個元件之間的狀態傳遞`
<!--SR:!2023-03-01,93,230-->

#🧠 React Context 可以取代元件的狀態傳輸和props嗎？->->-> `並不能`
<!--SR:!2023-04-30,135,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：狀態、更新狀態函式的資料傳遞方式有使用props所建立的props chain和使用context，前者場景為將元件轉換成可重複使用的元件，後者場景為元件間傳遞過程要經歷過多的元件]]
References:
[[@sebmarkbageProvideMoreWays]]