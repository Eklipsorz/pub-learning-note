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
1.  將nested Route元件安置在component，再讓component被parent route元件所包含
	- parent route元件的path要添加\/\*
	- nested route元件的path設定，具體會以瀏覽器目前頁面所在的位置來定位
	- 其path定位方式是以目前所處的Parent Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。
```
<Route path='/welcome/*' element={<Welcome />}>

// Welcome component
<Routes>
	<Route path='new-user' element={<p>welcome string</p>} />
</Routes>
```

2. parent route元件直接包裹nested route元件，並搭配Outlet元件
	- parent route元件的path可以省略\/\*，
	- nested route元件的path設定，具體會以parent route所在的path來定位
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
		
[](https://cdn.discordapp.com/attachments/618094134481256479/1050450649977987082/lwf40W3.png)重點：
- Outlet 本身命名緣由為提供特定事物出去的通道。
- Outlet 是一個react-router-dom所提供的元件
	- 主要用途為告知目前 nested route元件要在parent route對應的元件的哪處來渲染nested route所指定的element渲染內容
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

3. 以parent route所設定的path來決定nested Route的path

比如parent route是設定path1\/\*，而nested route若設定path2，那麼實際上路徑會是path1/為主，也就是path1/path2


#### 舉例
假若要設定/path1/path2 對應元件為xxxxx1，就直接將nested route的path設定成/path2，不用設定成/path1/path2，因為系統會在nested Route的path定為假定為parent Route所擁有的path，也就是/path1/為開頭

`<Route path='/path1/*' element=xxxx />`

```
// component
<Routes>
  // nested route
 <Route path='path2' element={xxxxx1} />
<Routes />
```



## 複習

#🧠 react-router-dom ：v5 和 v6 分別使用什麼元件來實現能將使用者導向至指定頁面的功能？ ->->-> `v5 是 Redirect元件、v6 是 Navigate`
<!--SR:!2023-10-06,52,210-->

#🧠 react-router-dom ：v6 還有Redirect嗎？若沒有得用什麼替代？ ->->-> `取消掉Redirect 元件，得用Navigate元件替代`
<!--SR:!2023-06-28,125,250-->

#🧠 react-router-dom ：v6是使用Navigate元件來實現能將使用者導向至指定頁面的功能，請問主要導向原理是什麼？ ->->-> `將指定頁面的網址推到瀏覽紀錄stack之最上面`
<!--SR:!2023-07-04,130,250-->


#🧠 react-router-dom ：v6是使用Navigate元件來實現能將使用者導向至指定頁面的功能，主要導向原理是將指定頁面的網址推到瀏覽紀錄stack之最上面，具體實現會是哪兩種方法去實現 ->->-> `主要是用push方式或者replace方式來調整瀏覽紀錄`
<!--SR:!2023-07-12,135,250-->

#🧠 react-router-dom v6：如何透過Navigate語法來以replace方式變動瀏覽紀錄，其語法是？ ->->-> `<Navigate replace to=xxxx />`
<!--SR:!2023-05-13,36,210-->


#🧠  react-router-dom v6：如何透過Navigate語法來以push方式變動瀏覽紀錄，其語法是？ ->->-> `	<Navigate to=xxxxx />`
<!--SR:!2023-08-21,162,250-->


#🧠  react-router-dom v6：建立nested Route 元件方式，其原理有哪些？ ->->-> `1. 將nested Route元件安置在component，再讓component被parent route元件所包含、2.  parent route元件直接包裹nested route元件，並搭配Outlet元件`
<!--SR:!2023-09-30,187,250-->

#🧠  react-router-dom v6：建立nested Route 元件方式，其中之一為parent route元件直接包裹nested route元件，該方法能順利讓nested route 元件渲染對應的元件嗎 ->->-> `通常沒搭配Outlet元件，沒辦法順利渲染`
<!--SR:!2023-05-13,78,230-->

#🧠 react-router-dom v6：建立nested Route 元件方式，其中之一為parent route元件直接包裹nested route元件，該搭配Outlet元件能讓nested route 元件渲染對應的元件，主要為何可以成功渲染？為什麼一定要它->->-> `nested route 元件綁定的元件A沒指定說要在哪個頁面元件下呈現對應元件A，所以得搭配Outlet元件告知React哪個位置才是元件A要呈現的地方`
<!--SR:!2023-05-08,74,230-->

#🧠 react-router-dom v6 ：建立nested Route 元件有兩個方式，其中之一是將nested Route元件安置在component，再讓component被parent route元件所包含，具體流程是什麼？->->-> `- parent route元件的path要添加/* - nested route元件的path設定，具體會以瀏覽器目前頁面所在的位置來定位`
<!--SR:!2023-06-10,115,250-->


#🧠  react-router-dom v6 ：建立nested Route 元件有兩個方式，其中之一是將parent route元件直接包裹nested route元件，並搭配Outlet元件，具體流程會是什麼？ ->->-> `	- parent route元件的path可以省略/* - nested route元件的path設定，具體會以parent route所在的path來定位`
<!--SR:!2023-06-27,123,250-->


#🧠 react-router-dom v6 ：建立nested Route 元件有兩個方式，其中之一是將parent route元件直接包裹nested route元件，並搭配Outlet元件，具體流程中的parent route元件的path為何可以省略\/\*？ ->->-> `因為系統會直接以包裹的後裔route元件以及搭配parent route的path來定位來找`
<!--SR:!2023-08-22,160,250-->

#🧠 react-router-dom v6 ：將nested Route元件安置在component，再讓component被parent route元件所包含，具體流程中的parent route元件的path可以省略\/\*？為什麼？->->-> `不能，因爲parent route包含的後裔元件並不是route元件，沒辦法直接省略`
<!--SR:!2023-06-25,45,170-->



#🧠  react-router-dom v6 ：第一、將nested Route元件安置在component，再讓component被parent route元件所包含；第二、parent route元件直接包裹nested route元件，並搭配Outlet元件。這兩種方法通常會使用哪種，為什麼  ->->-> `通常會選擇第二種，由於可以將路由設定集中在同一個檔案，比較容易維護`
<!--SR:!2023-07-26,141,250-->

#🧠 react-router-dom v6 ：第一、將nested Route元件安置在component，再讓component被parent route元件所包含，語法會是什麼？ ->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670246075/blog/react/react-router/v6/nested-route/react-router-v6-nested-route-with-component_ryhana.png)
<!--SR:!2023-10-01,35,210-->

#🧠 react-router-dom v6 ：第二、parent route元件直接包裹nested route元件，並搭配Outlet元件，語法會是什麼？ ->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670246075/blog/react/react-router/v6/nested-route/react-router-v6-nested-route-with-parent-route_nk6b5b.png)
<!--SR:!2023-09-28,185,250-->

#🧠 outlet 命名緣由是什麼？->->-> `Outlet 本身命名緣由為提供特定事物出去的通道`
<!--SR:!2023-09-27,184,250-->

#🧠 react-router-dom v5 vs. v6：Route元件的path比對方式分別是什麼？->->-> `前者是使用fuzzy matching；後者是使用exact matching`
<!--SR:!2023-08-26,128,245-->

#🧠 react-router-dom：Outlet 是什麼樣用途的元件->->-> `主要用途為告知目前 nested route元件要在parent route對應的元件的哪處來渲染nested route所指定的element渲染內容`
<!--SR:!2023-09-21,180,250-->

#🧠  react-router-dom：Outlet 在 nested route 上會是以哪個頁面元件的特定位置來渲染？->->-> `直接以parent route對應的渲染元件為主`
<!--SR:!2023-10-04,189,250-->

#🧠 react-router-dom：Outlet的存不存在 在 nested route 上會是什麼關係？ ->->-> `	- 若存在Outlet元件就以出現位置來呈現 - 若不存在就不呈現`
<!--SR:!2023-07-14,133,250-->

#🧠 以下為 react-router-dom v6的範例，請說明nested route在parent route的對應元件之間的關係，最好要搭配有沒有outlet來說明![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670249192/blog/react/react-router/v6/nested-route/react-router-v6-nested-route-with-outlet_cuogqg.png) ->->-> `比如底下設定new-user的Route擁有welcome string這字串當作JSX元件，但router不知道要如何把這元件渲染在目前頁面的何處，目前頁面元件會是Welcome，就會在裡頭檢查是否存在Outlet這元件，若存在就以出現位置來呈現welcome string這字串；若不存在就不呈現`
<!--SR:!2023-07-05,130,250-->

#🧠 react-router-dom v6：建造一個nested route 的概念為何？ ->->-> `每一個Route都必須由Routes元件包裹、替parent Route元件的path設定fuzzy match、以parent route所設定的path來決定nested Route的path`
<!--SR:!2023-06-11,80,210-->


#🧠 react-router-dom v6：建造一個nested route 的概念為何？其中的替parent Route元件的path設定fuzzy match，具體為何？ ->->-> `由於每個Route的path為exact match，得設定成fuzzy match才能透過nested Route所設定的path值瀏覽到nested 元件和對應的路由設定`
<!--SR:!2023-06-14,117,250-->

#🧠  react-router-dom v6：建造一個nested route 的概念為何？其中的替parent Route元件的path設定fuzzy match，具體實現為啥是設定fuzzy match ->->-> `由於每個Route的path為exact match，得設定成fuzzy match才能透過nested Route所設定的path值瀏覽到nested 元件和對應的路由設定`
<!--SR:!2023-09-19,181,250-->



#🧠 react-router-dom v6：parent route元件直接包裹nested route元件，並搭配Outlet元件，其nested Route的path定位方式會是如何？->->-> `其path定位方式是以目前所處的Parent Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。`
<!--SR:!2023-07-08,109,246-->

#🧠 react-router-dom v6：將nested Route元件安置在component，再讓component被parent route元件所包含，其nested Route的path定位方式會是如何？ ->->-> `其path定位方式是以目前所處的Parent Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。 `
<!--SR:!2023-06-11,94,246-->

#🧠 react-router-dom v6：parent route元件直接包裹nested route元件，並搭配Outlet元件，其nested Route的path為何不用額外添加parent route的path就能延伸？ ->->-> `主要是定位就是以parent route的path為主`
<!--SR:!2023-12-08,196,246-->

#🧠 react-router-dom v6：將nested Route元件安置在component，再讓component被parent route元件所包含，其nested Route的path為何不用額外添加parent route的path就能延伸？ ->->-> `主要是定位就是以parent route的path為主`
<!--SR:!2023-08-18,134,246-->


#🧠 react-router-dom v6：假若要設定/path1/path2 對應元件為xxxxx1，就直接將nested route的path設定成/path2，那麼那要如何瀏覽到nested route的對應渲染元件xxxxx1![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1670250102/blog/react/react-router/v6/nested-route/react-router-v6-nested-route-with-component_clqra8.png) ->->-> ``
<!--SR:!2023-09-04,169,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References: