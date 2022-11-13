## 描述


### 
當使用者提交成功時，會作出以下事情來回應

1. 呈現成功訊息來告知使用者

2. 導向至特定頁面

3. 以modal來告知使用者


### 

programmatic navigation

> we wanna trigger a navigation action and navigate the user away programmatically in our code

  

it's not a link which the user clicks to navigate away

but it's some action triggered by our code, when some abreaction sending the entered data to a server finished. and in the end we probably wanna trigger this navigation action from inside

  

**when a user is redirected as a result of an action that occurs on a route**

###
useHistory：

1. 由react-router-dom所提供

2.

> but it's named like this because it allows us to change the browser history

The `useHistory` hook gives you access to the `history` instance that you may use to navigate.

  

3. 回傳history object

  

browser history => the history of pages we visited.

  

history object：

- 隸屬於react-router-dom 所提供的物件，操控browser history，其history會是由stack來存放每一次使用者所瀏覽過的網頁，越上面越是最近瀏覽過的頁面，最上面的頁面為目前頁面

- push方法：將指定頁面推送至page stack最上面來當作目前頁面

> which pushes a new page on the stack of pages, so a new page on our history of pages or we can navigate with replace method that replaces the current page

- replace 方法：將指定頁面取代page stack的最上面page

  

  

push vs. replace

1. push can go back with the back button to the page we're coming from

2. replace can't。

  

  

replace => redirect where we changed occurred page

push => add a new page



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: