## 描述

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