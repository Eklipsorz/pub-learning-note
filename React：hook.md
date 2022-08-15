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


## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: