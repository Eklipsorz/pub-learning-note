## 描述


> If you're using a data router like createBrowserRouter it is uncommon to use this component as it does not participate in data loading.

> Whenever the location changes, \<Routes\> looks through all its child routes to find the best match and renders that branch of the UI. \<Route\> elements may be nested to indicate nested UI, which also correspond to nested URL paths. Parent routes render their child routes by rendering an \<Outlet\>.


建立



當path設定為/blog的nested route元件因為URL為/blog而被觸發時，此時會有三個Route會被觸發而執行loader、action、render：
- 第一個Route
```
<Route path='/' element={<RootLayout />}>
```
- 第二個Route
```
Route path='blog' element={<BlogLayout />}>
```
- 第三個Route
```
<Route index element={<BlogPostsPage />} loader={postsLoader} />
```
```
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
```

- 這三個元件的渲染會以身為parent route所指定的畫面來定位
- 這三個元件在渲染上的關係看上去像是parent-child關係，但實際上三個元件本身並不會被當作是，只是



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





## 複習


---
Status: 
Tags:
Links:
References: