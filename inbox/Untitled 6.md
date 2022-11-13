## 描述


### 當使用者提交表格並成功時，處理方會有的反應

當使用者提交成功時，會作出以下事情來回應，以下事情可能會重疊。
1. 呈現成功訊息來告知使用者
2. 導向至特定頁面
3. 以modal來告知使用者


### 

programmatic navigation

> we wanna trigger a navigation action and navigate the user away programmatically in our code

  

it's not a link which the user clicks to navigate away

but it's some action triggered by our code, when some abreaction sending the entered data to a server finished. and in the end we probably wanna trigger this navigation action from inside

  

**when a user is redirected as a result of an action that occurs on a route**

### useHistory 

[[@react-routerReactRouterDeclarativea]]
> The `useHistory` hook gives you access to the `history` instance that you may use to navigate.

  

useHistory：
1. 由react-router-dom所提供

2.

> but it's named like this because it allows us to change the browser history




### browser history 是什麼？
[[@WebBrowsingHistory2022]]
> Web browsing history refers to the list of web pages a user has visited

重點：
- browser history 或者 history 在網頁上是指使用者曾經瀏覽過到現在的網站清單

### 在react-router-dom上的 history object

[[@react-routerReactRouterDeclarativea]]
>  The term “history” and "history object" in this documentation refers to the history package

[[@react-routerReactRouterDeclarativea]]
> The following terms are also used:


> The following terms are also used:
> -   “browser history” - A DOM-specific implementation, useful in web browsers that support the HTML5 history API
> -   “hash history” - A DOM-specific implementation for legacy web browsers
> -   “memory history” - An in-memory history implementation, useful in testing and non-DOM environments like React Native

> `history` objects typically have the following properties and methods:

> -   `push(path, [state])` - (function) Pushes a new entry onto the history stack
> -   `replace(path, [state])` - (function) Replaces the current entry on the history stack

重點：
- react-router-dom 上所能用的history 會是由其他第三方所提供的介面，專門存取使用者在瀏覽器的瀏覽紀錄
- react-router-dom 所提供的 history 物件會取用自以下三者
	- browser history ：DOM API 提供開發者存取browser history的介面
	- hash history
	- memory history
- 不論哪一種，history皆會以stack來表示，

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
[[@WebBrowsingHistory2022]]
[[@react-routerReactRouterDeclarativea]]