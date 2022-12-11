## 描述

讓React-router根據URL切換來發送對應請求的前置處理：自製擁有loader功能的BrowserRouter、將Router安裝至RouterProvider元件、


### 讓React-router根據URL切換來發送對應請求的前置處理



#### 問題&解法： loader 和 useLoaderData 技術不被預設的BrowserRouter所支援

loader 和 useLoaderData 技術不被預設的BrowserRouter所支援，換言之，無法讓Router根據URL切換來發送請求

解法是：
- 重新定義Routing並建立BrowserRouter，其中Routing中的每個Route都會有對應Loader來告知React哪些是要以Loader來執行。

步驟：
- [[自製擁有loader功能的BrowserRouter，根據Routing作法：單純使用JS語言體系的物件語法來表示Routing中的每個Route、使用JSX語言體系的元件語法來表示Routing中的每個Route]]
- 將對應Routing的Router元件安裝至App.js來進行Routing和渲染：
	- 將Router物件安裝至RouterProvider元件，使Router物件能夠正常在對應元件進行Routing和渲染
	- 對應RouterProvider安裝至App.js





### RouterProvider 用法
[[@RouterProviderV6]]

> All router objects are passed to this component to render your app and enable the rest of the APIs.

```
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    children: [
      {
        path: "dashboard",
        element: <Dashboard />,
      },
      {
        path: "about",
        element: <About />,
      },
    ],
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <RouterProvider
    router={router}
    fallbackElement={<BigSpinner />}
  />
);
```


RouterProvider 元件
- 本身由react-router-dom函式庫所提供的函式
- 用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染：
	- 如何設定誰能夠使用對應Routing進行渲染，將Provider放至至特定元件就能允許。
- 本身語法是如下，不會加入任何元件
`<RouterProvider router=xxxxx/>`


  


  

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
[[@RouterProviderV6]]

