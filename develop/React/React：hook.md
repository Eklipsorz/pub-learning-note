## 描述


> tell React that is should run it (re-render) again, we need to import something from the React Library:
> 
> - useState: allow us to define values as state where changes to these values should reflect in the component function being called again

定義某些值為狀態，然後

  

useState

1. 是一種hook
2. create a special kind of variable. The variable where changes will lead this component function to be called again.
3. And of course we can therefore assign an initial value for that special variable

  
### hooks

  

> react hooks：
> 1. can be recognized by the fact that they start with the word "use" in their name
> 2. and these hooks must only be called inside of react component function like ExpenseItem
> 3. they can't be called outside of these functions, like this.


重點：
- react hook 名稱都以use開頭來命名
- react hook 都放置在元件對應的函式上，不可放在函式外


## sequelize hook 功能

hook 在原意上的名詞會是用做抓住某些東西的裝置，而動詞則是指用前者描述的裝置來抓住，若套用在電腦科學上，名詞會是描述著用來攔截函式呼叫、事件、訊息的代碼X，同時代碼也描述如何處理這些呼叫、事件、訊息，而這代碼就像是鉤子去準備釣(監聽並攔截)某個程式模組上的事件、函式呼叫、訊息，當發生該事件、函式呼叫、訊息時，此時鉤子就上釣獵物並按情況去執行鈎子內部的處理。

  

若是在套用在電腦科學上的動詞和動名詞，則是分別描述著代表著鈎子的代碼X抓住(處理)某個事件、函式呼叫、訊息和代表著鉤子的代碼X如何抓住(如何處理)某個事件、函式呼叫、訊息。

> NOUN IN DICTIONARY: a curved device used for catching or holding things

> VERB IN DICTIONARY: catch something with a hook

> NOUN IN CS: Code that handles such intercepted function calls, events or messages is called a hook.

> NOUN IN CS: Essentially it's a place in code that allows you to tap in to a module to either provide different behavior or to react when something happens.

  

舉例來說：假設我們替一個process建立一個程式模組X能夠從process攔截到特定事件來做出處理，而這個程式模組X就是鉤子，他就如同字面上的意思那樣在process裡放起鉤子，等待著(魚上鉤)事件發生

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650974362/blog/event/hook/put-a-hook-diagram_tfyvbf.png)

當事件發生時，鉤子便會執行對應事件處理來處理著這事件。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650974362/blog/event/hook/hooking-diagram_dl0hyp.png)


### 
hook 動詞：
> to fasten something with a hook, hang something on a hook, or catch something with a hook

hook 名詞：
> a curved device used for catching or holding things, especially one attached to a surface for hanging things on


重點
- hook 名詞：一種搭配彎勾來捕捉東西的工具
- hook 動詞：使用hook這工具來捕捉某些東西，捕捉到可以選擇放生或者做處理

### hook 在CS會是什麼意思？
[[@wanglingzhimaoFengSiXin65TiaoXiaoXi]]
> 这两个不是一个维度的东西，没有异同的概念。

> Callback 是一种异步调用的实现，打个比方，你希望让你的异地的同事帮助你完成某项工作，为了保证你们业务衔接流畅，你留了你的电话让他有进展和你联系（即Callback函数），那么随着事情的推进，你的同事会不断的打电话跟进让你知道那边的情况，这就是一种异步回调；C**allback 本意就是你传递一个函数给对方，当对方的工作有进展的时候就调用这个函数通知你**。

> Hook 则是一种 API 拦截手段，就比如一个公司有两个部门，他们平时会各指派一个业务对接人（API接口）去沟通彼此工作；但是某天因为业务调整，他们之间有一些事务需要外包出去，外包的事项是由你临时代为沟通，两边的对接人都不知道具体详情；为了避免混乱，此时你被作为一个中间人介入，切断原来两个部门之间的联系，他们的联络人都先和你沟通，由你决定哪些事情需要外包，哪些事情需要转达到另一个部门，这时候你就是一个Hook函数，拦截了原有的调用，并重新决定下一步的做什么，如果要继续原有流程也需要你代为转达。**Hook的特点就是不改变原有双边的逻辑的情况下，在API接口上插入一个拦截调用的Hook函数，从而截取调用数据、甚至可以改变程序行为。**

重點：
- callback 是用來實現非同步呼叫的回報結果實現，本意是當一個任務A要生成另一個非同步任務B來執行特定內容，並以函式C作為做完之後的回報方式或者結果處理，之後任務A和任務B都會做著自己的任務內容，等到任務B完成就執行函式C來處理完成結果/通報結果給任務A。


- hook 是一種多個程式模組間的攔截手段，具體會是在不改變每個模組的原有邏輯下插入一個攔截用模組來從而擷取這些模組互動的過程會有的資料、根據擷取結果來改變處理行為
- 用途為透過攔截來擷取程式模組間相互使用時的資料、根據擷取結果來改變處理行為
- 特點是可以在不改變模組上的原有邏輯上插入一個攔截用模組
- 原本在還沒引入hook時，每個模組會如同下圖的上面一樣，模組A可以直接呼叫模組B來執行；反之，模組B可以直接呼叫模組A。
- 引入hook之後，就如同下圖中的下面一樣，每個模組間的呼叫都有另一個模組C攔截，當模組A想呼叫模組B，必須透過模組C才能呼叫，模組B想呼叫模組A，就必須透過呼叫模組C才能呼叫模組A。
- 其中模組C會被稱之為hook function，負責攔截、收集資料、根據攔截結果來決定繼續讓模組AB能以原有邏輯(沒有hook下)服務著對方或者改變模組呼叫的結果。
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660573336/blog/react/hook/hook-before-after_gnjt9w.png)


## 複習
#🧠 hook 名詞 命名緣由為何 ->->-> `一種搭配彎勾來捕捉東西的工具`
<!--SR:!2025-01-08,540,250-->

#🧠 hook 動詞 命名緣由為何 ->->-> `使用hook這工具來捕捉某些東西，捕捉到可以選擇放生或者做處理`
<!--SR:!2023-10-09,43,210-->

#🧠 callback 是什麼？ ->->-> `是用來實現非同步呼叫的回報結果實現`
<!--SR:!2023-11-19,275,250-->

#🧠 callback 是什麼？ (以任務A、任務B、函式C來為例) ->->-> `本意是當一個任務A要生成另一個非同步任務B來執行特定內容，並以函式C作為做完之後的回報方式或者結果處理，之後任務A和任務B都會做著自己的任務內容，等到任務B完成就執行函式C來處理完成結果/通報結果給任務A。`
<!--SR:!2025-01-06,538,250-->

#🧠  在電腦科學裡，hook代表著什麼？->->-> `hook 是一種多個程式模組間的攔截手段，具體會是在不改變每個模組的原有邏輯下插入一個攔截用模組來從而擷取這些模組互動的過程會有的資料、根據擷取結果來改變處理行為`
<!--SR:!2024-06-23,409,250-->

#🧠 在電腦科學裡，hook的用途是什麼？ ->->-> `透過攔截來擷取程式模組間相互使用時的資料、根據擷取結果來改變處理行為`
<!--SR:!2024-01-30,196,230-->

#🧠 hook 的介入會破壞原有模組間的呼叫關係嗎？為何 ->->-> `會，因爲就是透過在模組間的呼叫關係之間插入一個另一個模組來攔截。`
<!--SR:!2024-11-27,513,250-->



#🧠 在電腦科學裡，hook的介入會破壞原有模組下的原有邏輯嗎？ ->->-> `並不會，但會影響呼叫關係，因為原有模組得透過hook才能恢復原有的呼叫關係`
<!--SR:!2023-10-16,161,230-->

#🧠 在電腦科學裡，原本在還沒引入hook時會是如何？請用下圖的before來說明 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660573336/blog/react/hook/hook-before-after_gnjt9w.png) ->->-> `每個模組會如同下圖的上面一樣，模組A可以直接呼叫模組B來執行；反之，模組B可以直接呼叫模組A。`
<!--SR:!2024-12-29,535,250-->

#🧠 在電腦科學裡，引入hook時會是如何？請用下圖的after來說明 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660573336/blog/react/hook/hook-before-after_gnjt9w.png) ->->-> `就如同下圖中的下面一樣，每個模組間的呼叫都有另一個模組C攔截，當模組A想呼叫模組B，必須透過模組C才能呼叫，模組B想呼叫模組A，就必須透過呼叫模組C才能呼叫模組A。`
<!--SR:!2024-12-18,518,250-->



#🧠 在電腦科學裡，after部分的Module C是什麼？做什麼用？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660573336/blog/react/hook/hook-before-after_gnjt9w.png) ->->-> `模組C會被稱之為hook function，負責攔截、收集資料、根據攔截結果來決定繼續讓模組AB能以原有邏輯(沒有hook下)服務著對方或者改變模組呼叫的結果。`
<!--SR:!2024-11-13,498,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]] - [[Operating System]]
Links:
References:
[[@wanglingzhimaoFengSiXin65TiaoXiaoXi]]