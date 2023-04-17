
## 描述

> ## [Unhandled rejections](https://javascript.info/promise-error-handling#unhandled-rejections)

> What happens when an error is not handled? For instance, we forgot to append `.catch` to the end of the chain, like here:



> In case of an error, the promise becomes rejected, and the execution should jump to the closest rejection handler. But there is none. So the error gets “stuck”. There’s no code to handle it.

>In practice, just like with regular unhandled errors in code, it means that something has gone terribly wrong.

> What happens when a regular error occurs and is not caught by `try..catch`? The script dies with a message in the console. A similar thing happens with unhandled promise rejections.

> The JavaScript engine tracks such rejections and generates a global error in that case. You can see it in the console if you run the example above.



## 複習
#🧠 JavaScript : 在Promise API時代中，若Promise內部執行的任務或者排程的任務拋出錯誤的話，系統會如何處理? (請考量到是否有Promise API語法所建立的錯誤處理)  ->->-> ``





#🧠 JavaScript : 以下p1為包裝特定任務的Promise object，若註冊後的事件處理拋出錯誤的話，那麼最後會如何執行![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681735097/blog/javascript/promise/Zalgo/promise-with-error-handler_vecbs1.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681735097/blog/javascript/promise/Zalgo/promise-with-error-handler_vecbs1.png) ->->-> `將拋出的錯誤包裝成rejected狀態的promise object，然後以該object來執行catch進行錯誤處理`


#🧠 JavaScript : 以下p1為包裝特定任務的Promise object，若註冊後的事件處理拋出錯誤的話，那麼最後會如何執行![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681735097/blog/javascript/promise/Zalgo/promise-without-error-handler_avjoze.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681735097/blog/javascript/promise/Zalgo/promise-without-error-handler_avjoze.png) ->->-> `將拋出的錯誤包裝成rejected狀態的promise object，但由於後續沒catch或者then所構成的錯誤處理，這會使得該promise object`

---
Status: #🌱 
Tags:
[[Promise]]
Links:
References: