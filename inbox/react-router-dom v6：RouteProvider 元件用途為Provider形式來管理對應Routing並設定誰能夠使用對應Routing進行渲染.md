## 描述

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
- 本身由react-router-dom函式庫所提供的元件
- 用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染：
	- 如何設定誰能夠使用對應Routing進行渲染，將Provider放至至特定元件就能允許。
- 本身語法是如下，不會加入任何元件：
	- router 是填入儲存對應routing的router物件，主要定義對應routing
`<RouterProvider router=router1/>`

## 複習

#🧠 react-router-dom v6： RouteProvider 會是什麼？->->-> `本身由react-router-dom函式庫所提供的元件`

#🧠 react-router-dom v6： RouteProvider 會是由react-router-dom函式庫所提供的元件，其用途會是什麼？->->-> `用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染`

#🧠 react-router-dom v6： RouteProvider 會是由react-router-dom函式庫所提供的元件，用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染，那麼具體如何設定誰能夠使用對應Routing進行渲染 ->->-> `將Provider放至至特定元件就能允許`

#🧠  react-router-dom v6： RouteProvider 語法是什麼->->-> `<RouterProvider router=router1/>`

#🧠 react-router-dom v6： RouteProvider 語法是`<RouterProvider router=router1/>`，其中的router會是什麼？->->-> `router 是填入儲存對應routing的router物件，主要定義對應routing`



---
Status: #🌱 
Tags:
[[React]]
Links:
[[讓React-router根據URL切換來發送對應請求的前置處理：主要有重新定義Routing並建立BrowserRouter、將對應Routing的Router元件安裝至App.js來進行Routing和渲染]]
[[自製擁有loader功能的BrowserRouter，根據Routing作法：單純使用JS語言體系的物件語法來表示Routing中的每個Route、使用JSX語言體系的元件語法來表示Routing中的每個Route]]
[[useLoaderData是react-router v6.4 所提供的hook，其概念為會從元件所待的目前Route元件獲取loader屬性並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料]]
References:
[[@RouterProviderV6]]