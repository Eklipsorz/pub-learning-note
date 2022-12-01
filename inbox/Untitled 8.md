## 描述



### v5 vs. v6： 能將使用者導向至指定頁面的元件

v5：
- 使用Redirect 元件來實現

v6：
- 取消掉Redirect元件
- 使用Navigate元件：
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
2. parent route元件直接包裹nested route元件

  
#### 第二種方式的好處
透過第二個方式可以將路由設定都集中在同一個檔案，增加維護性


### v6 ：一個nested route 打造方式

1. 每一個Route都必須由Routes元件包裹：添加Routes元件來包裹nested Route
```
<Routes>
 <Route path='/path1/path2' />
<Routes />
```
2. 替parent Route元件的path設定fuzzy match：由於每個Route的path為exact match，得設定成fuzzy match才能透過nested Route所設定的path值瀏覽到nested 元件和對應的路由設定

比如說path1的Route A包含著xxxx元件，而xxxx元件本身有Route B，在這裡由於xxxx元件被整個Route A包裹著，所以也可以將Route B 元件當成nested Route元件，為了能讓使用者透過nested route所設定的path來到xxxx元件找到Route B，得讓parent route的path增加\/\*來讓以\/path1\/開頭的任意字元放行近來。
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
### Link 和 Route

Link 和 Route 元件的定位方式是以目前所處的Route元件所擁有的path來定位 ，是直接假定parent route所設定的path來定位並當作開頭，所以不需要額外添加。

  

v5：link 和 route元件的定位方式一律是以瀏覽器目前頁面所在的位置來定位或者以主機所在的位置來定位，也就是維持著瀏覽器的relative url 和 absolute url規則來定位




## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: