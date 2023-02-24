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
	- 內建按鈕事件處理，當按下ok就允許導向頁面；當按下cancel就取消導向
- 該元件會監聽使用者是否透過目前頁面的任意元件切換成另一個網址，若有的話，可依據情況在切換前以一個對話視窗來阻擋使用者切換，若沒有的話，就允許使用者切換
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
1. Prompt 元件所能攔截到的navigation只能是它所在的頁面元件內所發出來的navigation請求/操作
2. 無法攔截 **單純以瀏覽器的網址欄位來輸入指定網址所進行單方面的網頁移動**，原因為：
	- 因它本身並不是透過使用特定地點A的任意事物給導向至特定地點B


### Prompt

> a message on a video screen that requests the operator to enter information or a command

> a sign on a computer screen that shows that the computer is ready to receive your instructions

重點：
- prompt 在電腦科學裡會是指顯示在螢幕上的訊息，該訊息會要求使用者輸入資訊或者指令
- 常見用途為：
	- 顯示一段訊息阻止使用者導向特定位置
## 複習

#🧠 prompt 在電腦科學裡會是什麼？ ->->-> `顯示在螢幕上的訊息，該訊息會要求使用者輸入資訊或者指令`
<!--SR:!2023-03-11,74,250-->

#🧠 prompt 在電腦科學會是顯示在螢幕上的訊息，該訊息會要求使用者輸入資訊或者指令，用途會是什麼？？->->-> `顯示一段訊息阻止使用者導向特定位置`
<!--SR:!2023-05-03,81,230-->

#🧠 react-router-dom 所提供的prompt component在畫面上會是什麼？  ->->-> `是一個對話視窗，裡面會有訊息、按鈕(ok、cancel)`
<!--SR:!2023-03-04,69,250-->

#🧠 prompt component 是由react-router-dom 所提供的元件，主要是一個對話視窗，裡面會有訊息、按鈕(ok、cancel) ，請問ok和cancel會需要設定事件處理嗎？為什麼？->->-> `不用，因內建按鈕事件處理，當按下ok就允許導向頁面；當按下cancel就取消導向`
<!--SR:!2023-04-12,90,249-->

#🧠 prompt component 是由react-router-dom 所提供的元件，主要是一個對話視窗，裡面會有訊息、按鈕(ok、cancel)，那麼它要如何阻止使用者從目前頁面導向另一個頁面內 ->->-> ` 該元件會監聽使用者是否透過目前頁面的任意元件切換成另一個網址，若有的話，可依據情況在切換前以一個對話視窗來阻擋使用者切換，若沒有的話，就允許使用者切換`
<!--SR:!2023-03-11,74,250-->

#🧠 react-router-dom ：Prompt componet 該元件會監聽使用者是否透過目前頁面的任意元件切換成另一個網址，若有的話，可依據情況在切換前以一個對話視窗來阻擋使用者切換，若沒有的話，就允許使用者切換，具體說明攔截部分->->-> `攔截Prompt所在的元件A內所發出來的navigation請求/操作，或者攔截使用者利用元件A的元件來發出navigation請求/操作`
<!--SR:!2023-03-15,71,230-->

#🧠 react-router-dom ：Prompt componet 的屬性主要有什麼->->-> `when、message`
<!--SR:!2023-05-20,112,249-->

#🧠 react-router-dom ：Prompt component 的屬性主要有什麼，其中when會是什麼型別？做什麼？？ ->->-> `布林值，true為當navigation就呈現prompt來組阻止從目前頁面跳轉；false為不使用prompt來阻止`
<!--SR:!2023-04-28,63,230-->


#🧠 react-router-dom ：Prompt componet 的屬性主要有什麼，其中message會是什麼型別？做什麼？？  ->->-> `字串或者function， 主要是指定prompt的主體訊息是什麼`
<!--SR:!2023-03-07,71,250-->

#🧠 react-router-dom ：Prompt componet 的屬性主要有什麼，其中message會採用function會是什麼？回傳什麼？ ->->-> ` location 是指使用者當前要跳轉的頁面位置、 action是指使用者當前對於瀏覽紀錄的操作是什麼。(location, action) => {}，會回傳字串或者true `
<!--SR:!2023-02-27,66,250-->

#🧠 react-router-dom ：Prompt componet 的屬性主要有什麼，其中message會採用function的話，其回傳內容代表什麼，具體說明 ->->-> `當使用function可以根據使用者對於瀏覽紀錄的操作和位置來定義後續處理，回傳內容正是指定prompt的主體訊息，若為true就允許導向`
<!--SR:!2023-05-14,110,249-->



#🧠 react-router-dom ：Prompt componet 的局限性是什麼？->->-> `Prompt 元件所能攔截到的navigation只能是它所在的頁面元件內所發出來的navigation請求/操作，無法攔截純以瀏覽器的網址欄位來輸入指定網址所進行單方面的網頁移動`
<!--SR:!2023-04-06,82,230-->

#🧠 react-router-dom ：Prompt componet為何無法阻止移動單純以瀏覽器的網址欄位來輸入指定網址所進行單方面的網頁？ ->->-> `因它本身並不是透過使用特定地點A的任意事物給導向至特定地點B`
<!--SR:!2023-05-15,110,249-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]
References:
[[@react-routerReactRouterDeclarativea]]