## 描述


### useRouteMatch hook 背景

使用Route 元件來實現conditional rendering 的缺點：
- path難以維護：
	- 主因為其Route的path會以parent Route元件的path為主，所以若parent Route更改path，就要連同更改child Route下的path，造成path難以維護


### useRouteMatch hook 使用


[[@react-routerReactRouterDeclarativea]]
> The useRouteMatch hook attempts to match the current URL in the same way that a \<Route\> would. It’s mostly useful for getting access to the match data without actually rendering a \<Route\>.

> takes no argument and returns the match object of the current `<Route>`

重點：
- useRouteMatch是由react-router-dom所提供的hook
- 主要回傳一個route match object
- route match 物件會夾雜著
	- path 屬性：目前元件所處的Route元件 A資訊
	- url 屬性：目前實際對應該元件A的URL資訊

### useRouteMatch hook 場景

實際使用useRouteMatch的場景是在：
1. nested route + conditional rendering


###  useRouteMatch 回傳的 route match 物件 調用的方式

```
1.    <Route path={`/quotes/${params.quoteId}/comments`}>
2.          <Comments />
3.    </Route>
```

以上面為例

使用方式為：
1. 使用placeholder來設定：具體是用match.path
```
1.  const match = useRouteMatch();
2. 
3.  <Route path={`${match.path}/comments`}>
4.       <Comments />
5.  </Route>
```
2. 使用具體的URL來實現match：具體適用match.url
```
1.  const match = useRouteMatch();
2.
3.  <Route path={`${match.url}/comments`}>
4.       <Comments />
5.  </Route>
```


### match.url 和 match.path 這兩者的場景
match.url 會是適用在hyperlink或者需要具體位置的場景
match.path 適用於以path為主的正規表達式來對應的場景




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]