## 描述


loader
[[@UseLoaderDataV6]]
> Each route can define a "loader" function to provide data to the route element before it renders.

> ## `params`

> Route params are parsed from [dynamic segments](https://reactrouter.com/en/main/route/route#dynamic-segments) and passed to your loader. This is useful for figuring out which resource to load:

```
createBrowserRouter([
  {
    path: "/teams/:teamId",
    loader: ({ params }) => {
      return fakeGetTeam(params.teamId);
    },
  },
]);
```

> Note that the `:teamId` in the path is parsed as provided as `params.teamId` by the same name.

> ## `request`
> Without React Router, the browser would have made a _Request_ to your server, but React Router prevented it! Instead of the browser sending the request to your server, React Router sends the request to your loaders.



loader 本身函式：
- 定義在每個Route元件上的loader屬性(attribute)
- 主要在Router渲染指定元件前，由Router負責執行loader來發出請求獲取資料，等到拿到資料，才去做渲染元件。
- 函式的參數為物件，物件主要有：
	- request 屬性：從當使用者在客戶端透過URL切換向伺服器發送請求對應URL的頁面時，react-router會攔截該請求並由它負責產生對應URL的頁面，同時會將request轉換成物件來當作這裡的屬性，通常request物件會包含請求封包本身，比如說當使用者透過URL切換來藉此向伺服器索求對應URL的頁面，Router會攔截該請求，並由它幫忙轉換對應頁面。
	- params 屬性： 目前react-router在目前所在Route攔截到的URL parameters部分

params 是物件，裡面夾雜了目前所處Route所攔截到的URL參數部分

```
1.  function loader(obj) {
2.  }

4.  obj = {
5.     params：  ...,
6.     request：....
7.  }
```
 - loader 本身主要會回傳以Promise為主的資料請求
## 複習

#🧠 react-router v6.4： loader 在Route元件上會是做什麼？->->-> `主要在Router渲染指定元件前，由Router負責執行loader來發出請求獲取資料，等到拿到資料，才去做渲染元件`
<!--SR:!2023-03-30,68,250-->

#🧠 react-router v6.4：loader 用途為主要在Router渲染指定元件前，由Router負責執行loader來發出請求獲取資料，等到拿到資料，才去做渲染元件，那麼它本身會如何設定在Route元件上？->->-> `每個Route元件的loader屬性(attribute)`
<!--SR:!2023-04-06,73,250-->

#🧠 react-router v6.4：loader 本身函式的參數會是什麼？ ->->-> `物件`
<!--SR:!2023-04-24,61,190-->

#🧠 react-router v6.4：loader 本身函式的參數會是物件，其物件主要會有哪些屬性？ ->->-> `request 屬性、params 屬性`
<!--SR:!2023-07-20,135,250-->

#🧠 react-router v6.4：loader 本身函式的參數會是物件，其物件主要會有哪些屬性？其中的request屬性會是什麼？ ->->-> `從當使用者在客戶端透過URL切換向伺服器發送請求對應URL的頁面時，react-router會攔截該請求並由它負責產生對應URL的頁面，同時會將request轉換成物件來當作這裡的屬性，通常request物件會包含請求封包本身，比如說當使用者透過URL切換來藉此向伺服器索求對應URL的頁面，Router會攔截該請求，並由它幫忙轉換對應頁面。`
<!--SR:!2023-03-18,60,250-->

#🧠 當使用者在客戶端透過URL切換向伺服器發送請求對應URL的頁面時，若沒有react-router的話，會是如何？ ->->-> `會直接向對應伺服器索要對應URL的頁面`
<!--SR:!2023-03-29,67,250-->

#🧠 當使用者在客戶端透過URL切換向伺服器發送請求對應URL的頁面時，若有react-router的話，會是如何？ ->->-> `react-router會攔截該請求，並由它負責將對應URL的頁面轉交給客戶端`
<!--SR:!2023-03-21,62,250-->

#🧠 react-router v6.4：loader 本身函式的參數會是物件，其物件主要會有哪些屬性？其中的params 屬性會是什麼？  ->->-> `目前react-router在目前所在Route攔截到的URL parameters部分`
<!--SR:!2023-04-07,74,250-->

#🧠 react-router v6.4：loader 本身函式定義語法會是如何？以params或者request屬性為例 ->->-> `function loader({ params }) {}、function loader({ request })`
<!--SR:!2023-06-15,113,250-->

#🧠 react-router v6.4：loader 本身通常會回傳什麼？->->-> `回傳一個promise為主的資料索求請求`
<!--SR:!2023-03-23,64,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@UseLoaderDataV6]]