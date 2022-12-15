
## 描述


### 自製擁有loader功能的BrowserRouter

根據Routing作法，主要有兩種做法：
- 單純使用JS語言體系的物件語法來表示Routing中的每個Route
- 使用JSX語言體系的元件語法來表示Routing中的每個Route，然後再將JSX語言體系轉換成JS語言體系的物件語法。



#### createBrowserRouter 用途

[[@CreateBrowserRouterV6]]
> This is the recommended router for all React Router web projects. It uses the DOM History API to update the URL and manage the history stack.
> It also enables the v6.4 data APIs like loaders, actions, fetchers and more.

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

createRoutesFromElements ：
- 屬於react-router-dom函式庫的函式
- 用途為允許開發者以JSX形式來定義Routing並建立對應的Router，具體是藉由將JSX語言體系的 Route 元件轉換成 JS語言體系的 Route 物件
- 語法為：
	- 回傳代表存有Route物件的陣列
	- 其中JSX Element為JSX語言體系的JSX Element
```
createRoutesFromElements(JSX Element)
```




  

### Route 元件的index屬性

> index routes are simply the default routes that will be rendered if the parent route path is activated


index屬性：
- index 屬性為Route元件所擁有的
- 若在Route元件添加index屬性，就會於當它所在的parent route被滿足時，會以標記index的Route元件所對應的頁面元件來預設渲染
- 每個被綁定index屬性的Route元件並不會有path屬性







### 範例

首先透過createBrowserRouter來建立擁有loader機制的Router，其中Routing會是以對應RootLayout元件的Route元件來擔任所有Route元件的Parent Route元件，後裔元件會以該元件的對應畫面為主，所以得在RootLayout定義Outlet元件才能確定每個後裔元件的渲染所在。

另外當瀏覽到/時，就會以RootLayout元件和WelcomePage元件來渲染，而當瀏覽到/blog時，系統會從中找到blog的Route，並將BlogPostsPage元件渲染在RootLayout元件的指定位置上。

```
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path='/' element={<RootLayout />}>
      <Route index element={<WelcomePage />} />
      <Route path='blog' element={<BlogLayout />}>
        <Route index element={<BlogPostsPage />} loader={blogPostsLoader} />
        <Route path=':id' element={<PostDetailPage />} />
      </Route>
      <Route path='blog/new' element={<NewPostPage />} />
    </Route>,
  ),
);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```
RootLayout 元件
```
import MainNavigation from '../components/MainNavigation';
import { Outlet } from 'react-router-dom';
function RootLayout({ children }) {
  return (
    <>
      <MainNavigation />
      <main>
        <Outlet />
      </main>
    </>
  );
}

export default RootLayout;
```


#### 以RootLayout的配置來編排所有頁面元件

> in order for rootlayout to support child routes,

> marks where all those nested child components

在這裏會以RootLayout的配置來編排所有頁面元件，然而在這裡的頁面元件皆會被RootLayout元件所包含，所以會以RootLayout指定的頁面元件為基底來渲染，但唯一問題就是不知道在那個頁面下的哪個位置進行渲染，所以得用Outlet來指定後裔Route元件可以在哪渲染他們所對應的頁面元件。

## 複習



#🧠 react-router-dom v6：使用createBrowserRouter 來自製擁有loader功能的BrowserRouter，根據Routing做法，可以有哪兩種做法？ ->->-> `- 單純使用JS語言體系的物件語法來表示Routing中的每個Route - 使用JSX語言體系的元件語法來表示Routing中的每個Route，然後再將JSX語言體系轉換成JS語言體系的物件語法。`
<!--SR:!2022-12-20,6,248-->

#🧠 react-router-dom v6：使用createBrowserRouter 來自製擁有loader功能的BrowserRouter，根據Routing做法，可以有哪兩種做法？其中可以使用JSX語言體系的元件語法來表示Routing中的每個Route，那這樣就能定義了？還是要做什麼？ 沒做會如何？->->-> `還得將JSX語言體系轉換成JS語言體系的物件語法。沒做的話，系統會無法正常執行`
<!--SR:!2022-12-20,6,248-->

#🧠 react-router-dom v6：createBrowserRouter 用途為何？->->-> `用途制定一組Routing來產生BrowserRouter`
<!--SR:!2022-12-20,6,248-->

#🧠 react-router-dom v6：createBrowserRouter 用途是制定一組Routing來產生BrowserRouter，那麼它屬於？？ ->->-> `屬於react-router-dom函式庫中的函式`
<!--SR:!2022-12-19,5,248-->

#🧠  react-router-dom v6：createBrowserRouter 用途是制定一組Routing來產生BrowserRouter，語法會是什麼？ ->->-> `const router = createBrowserRouter(paths)`
<!--SR:!2022-12-20,6,248-->

#🧠  react-router-dom v6：createBrowserRouter 用途是制定一組Routing來產生BrowserRouter，語法會是`const router = createBrowserRouter(paths)`，那麼paths會是什麼？  ->->-> `引數為陣列，陣列中的每個項目皆為一個能代表Route元件的Route物件`
<!--SR:!2022-12-20,6,248-->


#🧠  react-router-dom v6：createBrowserRouter 用途是制定一組Routing來產生BrowserRouter，語法會是`const router = createBrowserRouter(paths)`，它會回傳什麼？ ->->-> `回傳router物件`
<!--SR:!2022-12-20,5,248-->

#🧠 react-router-dom v6：createBrowserRouter 用途是制定一組Routing來產生BrowserRouter，語法會是`const router = createBrowserRouter(paths)`，那麼paths會是為陣列，陣列中的每個項目皆為一個能代表Route元件的Route物件，每個Route物件會是擁有什麼屬性？->->-> `	- path 為指定哪個path要比對和渲染 - element：當目前URL切換到Route物件所對應的path時，所要渲染的元件內容 - loader：當目前URL切換到Route物件所對應的path時，所要執行的資料載入或者對特定伺服器發送索要資料的請求，並於渲染之前回傳結果給元件 - children：以陣列來表示該對應Route元件所擁有的後裔Route元件。`
<!--SR:!2022-12-20,6,248-->


#🧠 react-router-dom v6：createRoutesFromElements 用途為何？ ->->-> `允許開發者以JSX形式來定義Routing並建立對應的Router`
<!--SR:!2022-12-20,6,248-->


#🧠 react-router-dom v6：createRoutesFromElements 用途為允許開發者以JSX形式來定義Routing並建立對應的Router，具體是什麼？->->-> `具體是藉由將JSX語言體系的 Route 元件轉換成 JS語言體系的 Route 物件`
<!--SR:!2022-12-19,5,248-->

#🧠 react-router-dom v6：createRoutesFromElements 語法為何？->->-> `createRoutesFromElements(JSX Element)`
<!--SR:!2022-12-19,5,248-->

#🧠 react-router-dom v6：createRoutesFromElements 語法為`createRoutesFromElements(JSX Element)`，那麼JSX Element會是什麼？->->-> `其中JSX Element為JSX語言體系的JSX Element`
<!--SR:!2022-12-15,3,250-->


#🧠 react-router-dom v6：createRoutesFromElements 會回傳什麼？->->-> `回傳代表存有Route物件的陣列`
<!--SR:!2022-12-15,2,230-->

#🧠 react-router-dom v6：Route 元件添加index屬性會是代表什麼？->->-> `就會於當它所在的parent route被滿足時，會以標記index的Route元件所對應的頁面元件來預設渲染`
<!--SR:!2022-12-19,5,248-->

#🧠 react-router-dom v6：`<Route path='/' element={<RootLayout />}>  <Route index element={<WelcomePage />} /> </Route>` 試著說明index的作用->->-> ``
<!--SR:!2022-12-19,5,248-->

#🧠 請試著說明每個路徑能夠對應到什麼以及渲染什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670789378/blog/react/react-router/v6/index-route/react-router-v6.4-with-index-route-example_rltcow.png) ->->-> ``
<!--SR:!2022-12-20,5,248-->


#🧠 裡頭的RootLayout元件對應的Route元件對於其他後裔元件來說，兩者渲染關係是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670789378/blog/react/react-router/v6/index-route/react-router-v6.4-with-index-route-example_rltcow.png)->->-> `在這裡會以RootLayout元件所對應的Route元件來當作是其他後裔Route元件的渲染參考頁面元件，並且會在RootLayout元件設定Outlet元件來告知React後裔Route元件的渲染可以在參考頁面上的哪個位置上做渲染`
<!--SR:!2022-12-21,6,248-->


#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-intro領取題目並切換至refactor-blogposts-page分支，請讓Router能夠根據切換URL來自行發送請求，並將請求回應丟給blogposts-page對應元件來接收並渲染->->-> `https://github.com/academind/react-router-6.4-intro/tree/react-router-6.4-basics/src`
<!--SR:!2022-12-21,6,248-->

#🧠 請問以下JSX元素經過createRoutesFromElements轉換後，會是什麼樣的語法？![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670856511/blog/react/react-router/Route-component/jsx-route-with-loader-example-_mhlbbh.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670856511/blog/react/react-router/Route-component/jsx-route-with-loader-example-_mhlbbh.png)->->-> `![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670856511/blog/react/react-router/Route-component/js-route-with-loader-example-_fpms3k.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670856511/blog/react/react-router/Route-component/js-route-with-loader-example-_fpms3k.png)`
<!--SR:!2022-12-15,2,248-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[useLoaderData是react-router v6.4 所提供的hook，其概念為會從元件所待的目前Route元件獲取loader屬性並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料]]
[[讓React-router根據URL切換來發送對應請求的前置處理：主要有重新定義Routing並建立BrowserRouter、將對應Routing的Router元件安裝至App.js來進行Routing和渲染]]
[[react-router-dom v6：RouteProvider 元件用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染]]
References:
[[@CreateBrowserRouterV6]]
[[@CreateRoutesFromElementsV6]]