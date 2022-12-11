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
	- 由React-router負責根據URL切換來發送對應請求來讓元件獲取資料或者服務，而非由元件負責發送請求。
	- 若Route A 設定loader屬性，當目前URL切換至對應Route A所對應的path，那麼就會由Router負責執行loader對應的請求處理，等到獲得回應才會將資料給予元件
```
<Route loader=.... />
```

#### 通常loader會定義在哪？

通常會將特定頁面A或者服務A相關的loader定義在特定頁面A或者服務A所對應的元件內，然後以named export來匯出

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




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[@UseLoaderDataV6]]
References: