## 描述


### 當使用者提交表格並成功時，處理方會有的反應

當使用者提交成功時，會作出以下事情來回應，以下事情可能會重疊。
1. 呈現成功訊息來告知使用者
2. 導向至特定頁面
3. 以modal來告知使用者


### programmatic navigation


> we wanna trigger a navigation action and navigate the user away programmatically in our code

重點：
- 以程式的手段來直接將使用者導向至特定頁面
- 手段通常會是使用history API或者操縱history的API

### useHistory 

[[@react-routerReactRouterDeclarativea]]
> The `useHistory` hook gives you access to the `history` instance that you may use to navigate.

  

useHistory：
1. 由react-router-dom所提供的hook
2. 專門回傳一個history 物件，該物件由另一個第三方而製成的history 物件，可藉由它來操縱瀏覽器的瀏覽紀錄。



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
- history 物件擁有的方法為：
	- push：將指定頁面路徑(path)推送至page stack最上面來當作目前頁面的路徑
	```
	history.push(path)
	```
	- replace：將指定頁面取代page stack的最上面來當作目前頁面的路徑
	```
	history.replace(path)
	```
- push vs. replace 差別：
	- 使用stack來調整瀏覽器時，是否可以回到原本的畫面：前者可以；後者不行，由於網址會被取代掉
	- 方式：前者是直接增加網址在最上面；後者則是將網址取代最上面

### browser history 是什麼？
[[@WebBrowsingHistory2022]]
> Web browsing history refers to the list of web pages a user has visited

重點：
- browser history 或者 history 在網頁上是指使用者曾經瀏覽過到現在的網站清單
- history上會是以多個頁面網址所構成的stack，越上面就越是最近瀏覽過的頁面網址，最上面為目前正在瀏覽的網址


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