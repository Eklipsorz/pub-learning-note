## 描述


### v5 vs. v6： 能將使用者導向至指定頁面的元件

v5：
- 使用Redirect 元件來實現

v6：
- 取消掉Redirect元件
- 使用Navigate元件：
	- 主要會是以瀏覽器目前頁面所在的位置來定位或者以主機所在的位置來定位
	- 以push 方式來導向：將指定頁面的網址xxxxx放到瀏覽紀錄stack的最上面
	```
	<Navigate to=xxxxx />
	```
	- 以replace 方式來導向：將指定頁面的網址取代瀏覽紀錄stack的最上面之網址
	```
	<Navigate replace to=xxxx />
	```

### 建立nested Route 元件方式
建立nested Route 元件有兩個方式：
1.  將nested Route元件安置在component，在讓component被parent route元件所包含
	- parent route元件的path要添加\/\*
	-  new-user的Route會是以它的parent route所在的path為主，也就是/welcome/new-user
	- 其path定位方式一律是以瀏覽器目前頁面所在的位置來定位或者以主機所在的位置來定位，也就是維持著瀏覽器的relative url 和 absolute url規則來定位
```
<Route path='/welcome/*' element={<Welcome />}>

// Welcome component
<Routes>
	<Route path='new-user' element={<p>welcome string</p>} />
</Routes>
```

2. parent route元件直接包裹nested route元件，並搭配Outlet元件
	- parent route元件的path可以省略\/\*
	- new-user的Route會是以它的parent route所在的path為主，也就是/welcome/new-user
	- 其path定位方式是以目前所處的Parent Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。
```
<Route path='/welcome' element={<Welcome />}>
	<Route path='new-user' element={<p>welcome string</p>} />
</Route>
```

  
#### 第二種方式的好處
透過第二個方式可以將路由設定都集中在同一個檔案，增加維護性



#### Outlet 元件

[[@react-routerReactRouterDeclarativea]]

> An `<Outlet>` should be used in parent route elements to render their child route elements. This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route.

outlet 命名緣由：
> a way, especially a pipe or hole, for liquid or gas to go out

重點：
- Outlet 本身命名緣由為提供特定事物出去的通道。
- Outlet 是一個react-router-dom所提供的元件
- 主要用途為告知目前 route元件要在哪處來渲染它對應的element內容，目前頁面會是以parent route 所對應的頁面元件，並且讓系統去該元件找尋Outlet元件來替代element內容進行渲染
	- 若存在Outlet元件就以出現位置來呈現
	- 若不存在就不呈現
- 舉例
	比如底下設定new-user的Route擁有welcome string這字串當作JSX元件，但router不知道要如何把這元件渲染在目前頁面的何處，目前頁面元件會是Welcome，就會在裡頭檢查是否存在Outlet這元件，若存在就以出現位置來呈現welcome string這字串；若不存在就不呈現
```
<Route path='/welcome' element={<Welcome />}>
	<Route path='new-user' element={<p>welcome string</p>} />
</Route>
```

```
import { Outlet, Link } from 'react-router-dom';

const Welcome = () => {
  return (
    <section>
      <h1>The Welcome Page</h1>
      <Link to='new-user'>Goto</Link>
      <Outlet />
    </section>
  );
};
```

### v6 ：建造一個nested route 的概念

1. 每一個Route都必須由Routes元件包裹：添加Routes元件來包裹nested Route
```
<Routes>
 <Route path='/path1/path2' />
<Routes />
```
2. 替parent Route元件的path設定fuzzy match：由於每個Route的path為exact match，得設定成fuzzy match才能透過nested Route所設定的path值瀏覽到nested 元件和對應的路由設定

比如說path1的Route A包含著xxxx元件，而xxxx元件本身有Route B，在這裡由於xxxx元件被整個Route A包裹著，所以也可以將Route B 元件當成nested Route元件，為了能讓使用者透過nested route所設定的path來到xxxx元件找到Route B，得讓parent route的path增加\/\*來讓以\/path1\/開頭的任意字元放行進來。
`<Route path='/path1/*' element=xxxx />`

xxxx 元件下的路由
```
<Routes>
 <Route path=path2 />
<Routes />
```

3. 以parent route所設定的path來決定nested Route的path：由於nested route的path本身會以parent route所設定的path為主，且不需要在nested route 的path再添加parent route所設定的path。

比如parent route是設定path1\/\*，而nested route若設定path2，那麼實際上路徑會是path1/為主，也就是path1/path2


#### 舉例
假若要設定/path1/path2 對應元件為xxxxx1，就直接將nested route的path設定成/path2，不用設定成/path1/path2，因為系統會在nested Route的path定為假定為parent Route所擁有的path，也就是/path1/為開頭

`<Route path='/path1/*' element=xxxx />`

```
<Routes>
  // nested route
 <Route path='path2' element={xxxxx1} />
<Routes />
```





## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-12-06,3,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References: