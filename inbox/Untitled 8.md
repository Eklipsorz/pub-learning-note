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
- prompt component 是由react-router-dom 所提供的元件，主要是一個對話視窗，裡面會有訊息、按鈕(ok、cancel)
- 該元件會監聽使用者是否從目前頁面切換成另一個頁面，若有的話，可依據情況在切換前以一個對話視窗來阻擋使用者切換，若沒有的話，就允許使用者切換
- 具體監聽會是攔截Prompt所在的元件A內所發出來的navigation請求/操作，或者攔截使用者利用元件A的元件來發出navigation請求/操作
- Prompt 元件的屬性為：
	- when：布林值，true為當navigation就呈現prompt來組阻止從目前頁面跳轉；false為不使用prompt來阻止
	- message：字串或者function
		- 主要是指定prompt的主體訊息是什麼，
		- 當使用function可以根據使用者對於瀏覽紀錄的操作和位置來定義後續處理，回傳內容正是指定prompt的主體訊息，若為true就允許導向
		- function語法為，會回傳字串或者true
			- location 是指使用者當前要跳轉的頁面位置
			- action是指使用者當前對於瀏覽紀錄的操作是什麼
```
(location, action) => {} 
```


#### Prompt元件的侷限性
1. Prompt 元件所能攔截到的navigation只能是它所在的元件內所發出來的navigation請求/操作
2. 無法攔截 **單純以瀏覽器的網址欄位來輸入指定網址所進行單方面的網頁移動**，原因為：
	- 單方面透過window物件來移動指定地點，本身並不是被特定地點A的任意事物給導向至特定地點B


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
[[navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]
References:
[[@react-routerReactRouterDeclarativea]]