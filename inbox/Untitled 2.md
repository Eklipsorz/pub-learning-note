## 描述

### Context 侷限問題

[[@sebmarkbageProvideMoreWays]]
> React Context is specifically not optimized for high frequency changes
> for example, if you have state changes every second or multiple times per second

> React Context also shouldn't be used to replaced all component communications and props


> component should still be configurable via props and short "props chains" might not need any replacement

[[@sebmarkbageProvideMoreWays]]
> My personal summary is that new context is ready to be used for low frequency unlikely updates (like locale/theme). It's also good to use it in the same way as old context was used. I.e. for static values and then propagate updates through subscriptions. It's not ready to be used as a replacement for all Flux-like state propagation.


重點：
- React Context 本身並沒有針對Context Value的高頻率變動做出較為優化的實現，目前停留在適用於Context Value變動頻率較低的場景下



## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：狀態、更新狀態函式的資料傳遞方式有使用props所建立的props chain和使用context，前者場景為將元件轉換成可重複使用的元件，後者場景為元件間傳遞過程要經歷過多的元件]]
References: