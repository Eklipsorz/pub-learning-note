## 描述

### 以React-router來用Loader來發送請求的前置處理

首先，預設的Router元件並不支援loader


### 

loader 和 useLoaderData 技術不被預設的BrowserRouter所支援，換言之，無法讓Router根據URL切換來發送請求


解法是：
- 自製一個

  

RouterProvider 元件

- 本身是如下，不會加入任何元件

`<RouterProvider router={}/>`

- 用途為Provider形式來管理對應Routing並設定誰能夠使用

  

> All router objects are passed to this component to render your app and enable the rest of the APIs.

  

  

createBrowserRouter

- 用途為制定一組Routing來產生BrowserRouter

  

  

createRoutesFromElements ：

- 將JSX語言體系的 Route 元件轉換成 JS語言體系的 Route 物件

- 用途為允許開發者以JSX形式來定義Routing並建立對應的Router

  

> `createRoutesFromElements` is a helper that creates route objects from `<Route>` elements.

> It's useful if you prefer to create your routes as JSX instead of objects.





###

index routes are simply the default routes that will be rendered if the parent route path is activated

  

  

Route元件的index 屬性若指定的話：就會於當它所在的parent route被滿足時，會以標記index的Route元件所對應的頁面元件來渲染


###

> in order for rootlayout to support child routes,

> marks where all those nested child components

在這裏會以RootLayout的配置來編排所有頁面元件，然而在這裡的頁面元件皆會被RootLayout元件所包含，所以會以RootLayout指定的頁面元件為基底來渲染，但唯一問題就是不知道在那個頁面下的哪個位置進行渲染，所以得用Outlet來指定後裔Route元件可以在哪渲染他們所對應的頁面元件。

## 複習


---
Status:  #🌱 
Tags:
[[React]]
Links:
[[useLoaderData是react-router v6.4 所提供的hook，其概念為會從元件所待的目前Route元件獲取loader屬性並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料]]
References: