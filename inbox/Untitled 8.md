## 描述

redirect 在react-router v6不存在

作為替代的元件為Navigate


1. Navigate元件實現push stack的用法
`<Navigate to=xxxxx />`
2. Navigate元件實現replace stack的用法
`<Navigate replace to=xxxx />`
### 


v6：nested route 打造方式

1. 每一個Route都必須由Routes元件包裹：添加Routes元件來包裹nested Route
```
<Routes>
 <Route path='/path1/path2' />
<Routes />
```
2. 替parent Route元件的path設定fuzzy match：由於每個Route的path為exact match，得設定成fuzzy match才能透過nested Route所設定的path值瀏覽到nested 元件和對應的路由設定

`<Route path='/path1/*' element=xxxx />`

xxxx 元件下的路由
```
<Routes>
 <Route path='/path1/path2' />
<Routes />
```

3. 將nested route的path以parent route所設定的path來定位：由於nested route的path本身會以parent route所設定的path為主，且不需要在nested route 的path再添加parent route所設定的path



假若要設定/path1/path2 對應元件為xxxxx1，就直接將nested route的path設定成/path2，不用設定成/path1/path2，因為系統會在nested Route的path定為假定為parent Route所擁有的path，也就是/path1/為開頭

`<Route path='/path1/*' element=xxxx />`

```
<Routes>
  // nested route
 <Route path='path2' element={xxxxx1} />
<Routes />
```
###

link 和 route 元件的定位方式是以目前所處的Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。

  

v5：link 和 route元件的定位方式一律是以瀏覽器目前頁面所在的位置來定位或者以主機所在的位置來定位，也就是維持著瀏覽器的relative url 和 absolute url規則來定位


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: