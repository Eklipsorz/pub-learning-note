## 描述


### 安置post-detail-page對應元件

```
import { useLoaderData } from 'react-router-dom';

import BlogPost from '../components/BlogPost';
import { getPost } from '../util/api';

function PostDetailPage() {
  const postData = useLoaderData();

  return (
    <>
      <BlogPost title={postData.title} text={postData.body} />
    </>
  );
}

export default PostDetailPage;

export function loader({ params }) {
  const postId = params.id;
  return getPost(postId);
}
```


### 安置每個路徑拋出錯誤時會有的畫面
```
import { useRouteError } from 'react-router-dom';
import MainNavigation from '../components/MainNavigation';

function ErrorPage() {
  const error = useRouteError();

  return (
    <>
      <MainNavigation />
      <main id="error-content">
        <h1>An error occurred!</h1>
        <p>{error.message}</p>
      </main>
    </>
  );
}

export default ErrorPage;
```


```
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<RootLayout />} errorElement={<ErrorPage />}>
      <Route index element={<WelcomePage />} />
      <Route path="/blog" element={<BlogLayout />}>
        <Route index element={<BlogPostsPage />} loader={blogPostsLoader} />
        <Route
          path=":id"
          element={<PostDetailPage />}
          loader={blogPostLoader}
        />
      </Route>
      <Route
        path="/blog/new"
        element={<NewPostPage />}
        action={newPostAction}
      />
    </Route>
  )
);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```
## 複習


#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-intro領取題目並切換成refactor-blogposts-and-post-page分支，請讓Router能夠根據切換URL來自行發送請求，並將請求回應丟給posts-page和post-detail-page對應元件來接收並渲染，記得要添加錯誤時會有的畫面 ->->-> `https://github.com/academind/react-router-6.4-intro/tree/react-router-6.4-basics/src/pages`
<!--SR:!2023-02-06,23,250-->


#🧠 ES module：若要取出匯出物件中的屬性且要替屬性取別名來擷取，請問如何做 ->->-> `使用as`



---
Status: #🌱 
Tags:
[[React]]
Links:
[[loader 本身函式會是定義在每個Route元件上的loader屬性，其作用為在Router渲染指定元件前，由Router負責執行loader來發出請求獲取資料，等到拿到資料，才去做渲染元件]]
[[errorElement 屬性用途是指定當Route的對應元件發生錯誤時所要渲染的畫面內容；useRouteError 用途則是專門從擷取到錯誤資訊物件的Router物件獲取對應錯誤資訊]]
References: