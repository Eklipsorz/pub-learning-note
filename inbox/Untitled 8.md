## 描述


> If you're using a data router like createBrowserRouter it is uncommon to use this component as it does not participate in data loading.

> Whenever the location changes, \<Routes\> looks through all its child routes to find the best match and renders that branch of the UI. \<Route\> elements may be nested to indicate nested UI, which also correspond to nested URL paths. Parent routes render their child routes by rendering an \<Outlet\>.


定義Routing的語法或者元件分別有以下：
	- createBrowserRouter 語法
	- Routes 元件
挑選路徑：
	- 當Routing還未定義時就遍歷每個Route並記錄每個Route元件的path
	- 遍歷每個Route元件擁有的path來比對使用者所輸入的URL並打上分數
	- 遍歷完畢就挑選分數最高的Route來執行對應loader、action、render

細節：
	- 元件最多只會挑選一個元件來渲染
	- 當nested Route所對應的path滿足使用者所輸入的URL時，會同時將 parent route的對應元件 和 nested Route的對應元件 合併成一個元件來渲染：
		- 以 parent route的對應元件為主，然後再由 parent route的對應元件指定哪個位置要渲染nested Route的對應元件。



```
import MainNavigation from '../components/MainNavigation';

function RootLayout({ children }) {
  return (
    <>
      <MainNavigation />
      <main>{children}</main>
    </>
  );
}

export default RootLayout;
```



```
import {
  Route,
  createRoutesFromElements,
  createBrowserRouter,
  RouterProvider,
} from 'react-router-dom';

import BlogLayout from './pages/BlogLayout';
import BlogPostsPage, { loader as postsLoader } from './pages/BlogPosts';
import NewPostPage from './pages/NewPost';
import PostDetailPage, { loader as postLoader } from './pages/PostDetail';
import RootLayout from './pages/RootLayout';
import WelcomePage from './pages/Welcome';

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path='/' element={<RootLayout />}>
      <Route index element={<WelcomePage />} />
      <Route path='blog' element={<BlogLayout />}>
        <Route index element={<BlogPostsPage />} loader={postsLoader} />
        <Route path=':id' element={<PostDetailPage />} loader={postLoader} />
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



## 複習


---
Status: 
Tags:
Links:
References: