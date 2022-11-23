## 描述


### 
使用Route 元件來實現conditional rendering 的缺點：主要由於其Route的path會以parent Route元件的path為主，所以若parent Route更改path，就要連同更改child Route下的path，造成path難以維護


###
useRouteMatch：

1. 由react-router-dom所提供的hook

2. 主要回傳一個location match object，該物件會夾雜目前元件所處的Route元件 A資訊和實際對應該元件A的URL資訊

  

-   takes no argument and returns the match object of the current `<Route>`
    

hook 直接取得目前正在渲染的頁面位置


### 

實際使用useRouteMatch的場景是在：

1. nested route + conditional rendering

  

另外在path這邊可以採用match.path 或者math.url 來替代成match.path/comments或者match.url/comments

```
1.    <Route path={`/quotes/${params.quoteId}/comments`}>
2.          <Comments />
3.    </Route>
```

1. 使用placeholder 來實現match
```
1.  const match = useRouteMatch();
2. 
3.  <Route path={`${match.path}/comments`}>
4.       <Comments />
5.  </Route>
```
  

2. 使用具體的URL來實現match
```
1.  const match = useRouteMatch();
2.
3.  <Route path={`${match.url}/comments`}>
4.       <Comments />
5.  </Route>
```


### 
match.url 會是適用在hyperlink或者需要具體位置的場景

match.path 適用於會拿來使用正規表達式來使用的場景


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: