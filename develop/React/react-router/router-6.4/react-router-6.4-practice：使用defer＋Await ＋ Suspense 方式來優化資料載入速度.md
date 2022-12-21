## 描述



### 問題描述

在瀏覽/blog對應元件前，會花費至少2秒鐘的資料載入時間才能對對應URL的元件進行渲染，若要優化資料載入的話，在這會使用defer＋Await ＋ Suspense 方式來解決


### 解決流程：
1. 在loader定義夾雜deferred promise的物件
2. 將loader回傳的deferred promise物件給元件做為Await來調用其promise請求的執行、並根據resolve來渲染
3. 將Suspense包覆在Await元件來設定處理前的畫面以及一些可在一開始渲染的元件




#### 在loader定義夾雜deferred promise的物件

```
export async function loader() {
  return defer({ getPosts: getSlowPosts() });
}
```


#### 將loader回傳的deferred promise物件給元件做為Await來調用其promise請求的執行、並根據resolve來渲染


```
import { useLoaderData, defer, Await } from 'react-router-dom';
import { Suspense } from 'react';

import Posts from '../components/Posts';
import { getSlowPosts } from '../util/api';

function DeferredBlogPostsPage() {
  const loaderData = useLoaderData();

  return (
      <Suspense fallback={<p>Loading...</p>}>
        <Await resolve={loaderData.getPosts} errorElement={<p>Error</p>}>
          {(posts) => <Posts blogPosts={posts} />}
        </Await>
      </Suspense>
  );
}
```



#### 將Suspense包覆在Await元件來設定處理前的畫面以及一些可在一開始渲染的元件
```
function DeferredBlogPostsPage() {
  const loaderData = useLoaderData();
  return (
    <>
      <h1>Our Blog Posts</h1>
      <Suspense fallback={<p>Loading...</p>}>
        <Await resolve={loaderData.getPosts} errorElement={<p>Error</p>}>
          {(posts) => <Posts blogPosts={posts} />}
        </Await>
      </Suspense>
    </>
  );
}
```


### 完整代碼

```
import { useLoaderData, defer, Await } from 'react-router-dom';
import { Suspense } from 'react';

import Posts from '../components/Posts';
import { getSlowPosts } from '../util/api';

function DeferredBlogPostsPage() {
  const loaderData = useLoaderData();

  return (
    <>
      <h1>Our Blog Posts</h1>
      <Suspense fallback={<p>Loading...</p>}>
        <Await resolve={loaderData.getPosts} errorElement={<p>Error</p>}>
          {(posts) => <Posts blogPosts={posts} />}
        </Await>
      </Suspense>
    </>
  );
}

export default DeferredBlogPostsPage;

export async function loader() {
  return defer({ getPosts: getSlowPosts() });
}
```



## 複習

#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-adv領取題目並切換至refactor-in-slow-loading分支，接著到DeferredBlogPosts.jsx解決以下問題：在瀏覽/blog對應元件前，會花費至少2秒鐘的資料載入時間才能對對應URL的元件進行渲染，請試著優化其載入速度->->-> `https://github.com/academind/react-router-6.4-intro/tree/react-router-6.4-adv`
<!--SR:!2022-12-25,3,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References: