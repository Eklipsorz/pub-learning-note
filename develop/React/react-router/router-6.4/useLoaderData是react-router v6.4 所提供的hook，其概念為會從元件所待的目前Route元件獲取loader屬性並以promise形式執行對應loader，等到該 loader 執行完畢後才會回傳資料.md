## 描述

[[@UseLoaderDataV6]]

> This hook provides the value returned from your route loader.

useLoaderData：
- react-router v6.4 所提供的hook
- 其概念為會從元件所待的目前Route元件獲取loader屬性(attribute)，並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料給對應元件
- 用法為如下
	-  useLoaderData 會是回傳loader 以resolve形式所回傳的資料
```
const loadedData = useLoaderData()
```
- 使用useLoaderData的目的為：
	- 由React-router負責根據使用者所切換的URL來發送對應請求來讓元件獲取資料或者服務，而非由元件負責發送請求。
	- 若Route A 設定loader屬性，當目前URL切換至對應Route A所對應的path，那麼就會由Router負責執行loader對應的請求處理，等到獲得回應才會將資料給予元件
```
<Route loader=.... />
```

#### 通常loader會定義在哪？

通常會將特定頁面A或者服務A相關的loader定義在特定頁面A或者服務A所對應的元件內，然後以named export來匯出，匯出形式會如下：
	- 該loader只能回傳promise
```
export function loader() {
  return getPosts();
}
```


```
import { useLoaderData } from 'react-router-dom';
import Posts from '../components/Posts';
import { getPosts } from '../util/api';

function BlogPostsPage() {
  const loadedData = useLoaderData();

  return (
    <>
      <h1>Our Blog Posts</h1>
      <Posts blogPosts={loadedData} />
    </>
  );
}

export default BlogPostsPage;
export function loader() {
  return getPosts();
}
```


```
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path='/' element={<RootLayout />}>
      <Route index path='/' element={<WelcomePage />} />
      <Route path='/blog' element={<BlogLayout />}>
        <Route index element={<BlogPostsPage />} loader={blogPostsLoader} />
        <Route path=':id' element={<PostDetailPage />} />
      </Route>
      <Route path='/blog/new' element={<NewPostPage />} />
    </Route>,
  ),
);

function App() {
  return <RouterProvider router={router} />;
}
```




## 複習

#🧠 react-router-dom v6：使用useLoaderData的目的為何？ ->->-> `由React-router負責根據使用者所切換的URL來發送對應請求來讓元件獲取資料或者服務，而非由元件負責發送請求。`
<!--SR:!2023-05-15,37,230-->

#🧠  react-router-dom v6：useLoaderData 是什麼？用途是什麼？ ->->-> `react-router v6.4 所提供的hook、用途為在元件所待的目前Route元件獲取loader屬性(attribute)，並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料給對應元件`
<!--SR:!2023-10-09,209,270-->

#🧠 react-router-dom v6：useLoaderData語法是什麼？ ->->-> `const loadedData = useLoaderData()`
<!--SR:!2023-10-06,183,250-->

#🧠 react-router-dom v6：useLoaderData語法是const loadedData = useLoaderData()，請問它會回傳什麼？？ ->->-> ` useLoaderData 會是回傳loader 以resolve形式所回傳的資料`
<!--SR:!2023-08-13,150,250-->



#🧠 useLoaderData 其概念為會從元件所待的目前Route元件獲取loader屬性(attribute)，並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料給對應元件，那麼loader會定義在哪？->->-> `通常會將特定頁面A或者服務A相關的loader定義在特定頁面A或者服務A所對應的元件內，然後以named export來匯出`
<!--SR:!2023-09-15,173,250-->



#🧠 useLoaderData 其概念為會從元件所待的目前Route元件獲取loader屬性(attribute)，並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料給對應元件，那麼loader會如何設定在Route元件？？->->-> `<Route loader={loader} />`
<!--SR:!2023-06-20,118,250-->

#🧠 useLoaderData 其概念為會從元件所待的目前Route元件獲取loader屬性(attribute)，並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料給對應元件，那麼loader的原型會是如何？舉例說明 ->->-> `具體會是promise，export function loader() { return getPosts(); }`
<!--SR:!2023-09-29,165,230-->


#🧠 react-router-dom v6： 請說明以下loader和element之間的關係 `<Route loader={ loader1 } element={<element />} />` ->->-> `目前URL切換至對應Route A所對應的path，那麼就會由Router負責執行loader對應的請求處理，等到獲得回應才會將資料給予元件`
<!--SR:!2023-10-01,182,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[讓React-router根據URL切換來發送對應請求的前置處理：主要有重新定義Routing並建立BrowserRouter、將對應Routing的Router元件安裝至App.js來進行Routing和渲染]]
[[自製擁有loader功能的BrowserRouter，根據Routing作法：單純使用JS語言體系的物件語法來表示Routing中的每個Route、使用JSX語言體系的元件語法來表示Routing中的每個Route]]
[[react-router-dom v6：RouterProvider 元件用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染]]
References:
[[@UseLoaderDataV6]]