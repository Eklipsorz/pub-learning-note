## 描述

[[@react-routerReactRouterDeclarativea]]

> Used to prompt the user before navigating away from a page. When your application enters a state that should prevent the user from navigating away (like a form is half-filled out), render a `<Prompt>`.


> message: func

> Will be called with the next location and action the user is attempting to navigate to. Return a string to show a prompt to the user or true to allow the transition.


> when: bool

> Instead of conditionally rendering a \<Prompt\> behind a guard, you can always render it but pass when={true} or when={false} to prevent or allow navigation accordingly.


```
<Prompt
  message={(location, action) => {
    if (action === 'POP') {
      console.log("Backing up...")
    }

    return location.pathname.startsWith("/app")
      ? true
      : `Are you sure you want to go to ${location.pathname}?`
  }}
/>
```


重點：
- prompt componentd 

1. 由react-router-dom所提供

2. 自動監測特定規則是否滿足，若滿足就呈現warning，若不滿足就不呈現。

3. Prompt 有兩個主要的attributes：

- when：布林值，true為渲染prompt來阻止從目前頁面跳轉；false為不使用prompt來阻止

> to finding whether this prompt should be shown if the user changes the URL or not

- message：字串或者function，主要是指定prompt的主體訊息是什麼，當使用function可以根據使用者對於瀏覽紀錄的操作和位置來定義後續處理，回傳內容正是指定prompt的主體訊息

=> (location, action) => {} 中的location 是指使用者當前要跳轉的頁面位置，action是指使用者當前對於瀏覽紀錄的操作是什麼

  

> this is a component which we can render. And then this component will automatically watch if we navigate away. And if then a certain condition is met, it will show a warning before it allows use to leave


### Prompt

> a message on a video screen that requests the operator to enter information or a command

> a sign on a computer screen that shows that the computer is ready to receive your instructions



重點：
- prompt 在電腦科學裡會是指顯示在螢幕上的訊息，該訊息會要求使用者輸入資訊或者指令

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:

References:
[[@react-routerReactRouterDeclarativea]]