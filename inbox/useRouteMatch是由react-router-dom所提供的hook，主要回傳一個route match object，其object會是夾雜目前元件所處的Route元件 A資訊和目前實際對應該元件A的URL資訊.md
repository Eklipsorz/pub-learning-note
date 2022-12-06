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
- useRouteMatch 會從目前對應到的parent route元件所擁有的路徑資訊取得其資訊，並回傳夾雜資訊的物件 - route match 物件
- route match 物件會夾雜著
	- path 屬性：目前對應到的Route元件所擁有的path屬性值，拿下面舉例的Component來說，就會是為path1
	```
	<Route path=path1>
		<Component1 />
	</Route>
	```
	- url 屬性：目前對應到的Route元件所取得的實際路徑值


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
2. 使用具體的URL來設定：具體適用match.url
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

#🧠 react-router-dom：useRouteMatch是什麼樣的hook->->-> `useRouteMatch 會從目前對應到的parent route元件所擁有的路徑資訊取得其資訊，並回傳夾雜資訊的物件`
<!--SR:!2022-12-09,11,250-->

#🧠 react-router-dom：useRouteMatch 會回傳route match 物件，其物件會是夾雜著什麼屬性？  ->->-> `path屬性、url屬性`
<!--SR:!2022-12-28,22,250-->

#🧠 react-router-dom：useRouteMatch 會回傳route match 物件，其物件會夾雜著path屬性、url屬性，這兩個屬性是什麼？ ->->-> `path 屬性：目前對應到的Route元件所擁有的path屬性值、url 屬性：目前對應到的Route元件所取得的實際路徑值`
<!--SR:!2022-12-07,9,250-->

#🧠  react-router-dom：假如在Component1設定useRouteMatch這hook，那麼會取得到的path和url會是什麼？\<Route path=path1\>  \<Component1 \/\> \<\/Route\>->->-> `path會是Route的path1，url則是Route元件獲取到的實際路徑`
<!--SR:!2022-12-08,10,250-->

#🧠 運用useRouteMatch 回傳的 route match 物件 調用的概念有哪些？ ->->-> `使用placeholder來設定、使用具體的URL來對應`
<!--SR:!2022-12-21,16,230-->

#🧠 useRouteMatch 回傳的 route match 物件 調用的概念會有使用placeholder來設定、使用具體的URL來對應 這些，那麼具體會是分別為何？ ->->-> `使用placeholder來設定：具體是用match.path、使用具體的URL來設定：具體適用match.url`
<!--SR:!2022-12-08,10,250-->


#🧠 useRouteMatch 回傳的 route match 物件 調用的概念會有使用placeholder來設定、使用具體的URL來對應 這些，這兩者適用場景為何？ ->->-> `match.url 會是適用在hyperlink或者需要具體位置的場景 match.path 適用於以path為主的正規表達式來對應的場景`
<!--SR:!2022-12-07,9,250-->

#🧠 useRouteMatch被提出的背景是什麼？ ->->-> `path難以維護`
<!--SR:!2022-12-07,9,250-->

#🧠 useRouteMatch被提出的背景是path難以維護，具體是什麼？ ->->-> `主因為其Route的path會以parent Route元件的path為主，所以若parent Route更改path，就要連同更改child Route下的path，造成path難以維護`
<!--SR:!2022-12-09,11,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]