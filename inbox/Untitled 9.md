
## 描述

### 自製擁有loader功能的BrowserRouter

根據Routing作法，主要有兩種做法：
- 單純使用JS語言體系的物件語法來表示Routing中的每個Route
- 使用JSX語言體系的元件語法來表示Routing中的每個Route，然後再將JSX語言體系轉換成JS語言體系的物件語法。



#### createRoutesFromElements 用途

[[@CreateBrowserRouterV6]]
> `createRoutesFromElements` is a helper that creates route objects from `<Route>` elements. It's useful if you prefer to create your routes as JSX instead of objects.

```
const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    loader: rootLoader,
    children: [
      {
        path: "team",
        element: <Team />,
        loader: teamLoader,
      },
    ],
  },
]);
```


```
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";


const router = createBrowserRouter(paths)
```


createBrowserRouter
- 屬於react-router-dom函式庫中的函式
- 用途制定一組Routing來產生BrowserRouter
- 語法為：
	- 回傳router物件
	- 引數為陣列，陣列中的每個項目皆為一個能代表Route元件的Route物件，物件基本會有path、element、loader、children這四個屬性：
		- path 為指定哪個path要比對和渲染
		- element：當目前URL切換到Route物件所對應的path時，所要渲染的元件內容
		- loader：當目前URL切換到Route物件所對應的path時，所要執行的資料載入或者對特定伺服器發送索要資料的請求，並於渲染之前回傳結果給元件
		- children：以陣列來表示該對應Route元件所擁有的後裔Route元件。
```
const router = createBrowserRouter(paths)
```



```
const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    loader: rootLoader,
    children: [
      {
        path: "team",
        element: <Team />,
        loader: teamLoader,
      },
    ],
  },
]);
```


#### createRoutesFromElements 用途
[[@CreateRoutesFromElementsV6]]
> `createRoutesFromElements` is a helper that creates route objects from `<Route>` elements.
> It's useful if you prefer to create your routes as JSX instead of objects.

createRoutesFromElements ：
- 屬於react-router-dom函式庫的函式
- 將JSX語言體系的 Route 元件轉換成 JS語言體系的 Route 物件
- 用途為允許開發者以JSX形式來定義Routing並建立對應的Router


  
```
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

// You can do this:
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<Root />}>
      <Route path="dashboard" element={<Dashboard />} />
      <Route path="about" element={<About />} />
    </Route>
  )
);

// Instead of this:
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
```

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
[[useLoaderData是react-router v6.4 所提供的hook，其概念為會從元件所待的目前Route元件獲取loader屬性並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料]]
[[Untitled 8]]
References:
[[@CreateBrowserRouterV6]]
[[@CreateRoutesFromElementsV6]]