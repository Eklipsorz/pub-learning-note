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
- hook 動詞：使用hook這工具來捕捉某些東西

### 

  

> 这两个不是一个维度的东西，没有异同的概念。

> Callback 是一种异步调用的实现，打个比方，你希望让你的异地的同事帮助你完成某项工作，为了保证你们业务衔接流畅，你留了你的电话让他有进展和你联系（即Callback函数），那么随着事情的推进，你的同事会不断的打电话跟进让你知道那边的情况，这就是一种异步回调；C**allback 本意就是你传递一个函数给对方，当对方的工作有进展的时候就调用这个函数通知你**。

> Hook 则是一种 API 拦截手段，就比如一个公司有两个部门，他们平时会各指派一个业务对接人（API接口）去沟通彼此工作；但是某天因为业务调整，他们之间有一些事务需要外包出去，外包的事项是由你临时代为沟通，两边的对接人都不知道具体详情；为了避免混乱，此时你被作为一个中间人介入，切断原来两个部门之间的联系，他们的联络人都先和你沟通，由你决定哪些事情需要外包，哪些事情需要转达到另一个部门，这时候你就是一个Hook函数，拦截了原有的调用，并重新决定下一步的做什么，如果要继续原有流程也需要你代为转达。**Hook的特点就是不改变原有双边的逻辑的情况下，在API接口上插入一个拦截调用的Hook函数，从而截取调用数据、甚至可以改变程序行为。**

重點：
- hook 是一種多個程式模組間的攔截手段


## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: