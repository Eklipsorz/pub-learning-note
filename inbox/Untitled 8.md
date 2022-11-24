## 描述


Route 的path 寫法：盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑。
實現方式為：
- 使用useRouteMatch 從目前對應的parent route元件中取得路徑和實際路徑
- 使用useLocation 從目前頁面中取得實際路徑


### 場景：使用useRouteMatch 和 使用useLocation
1. useRouteMatch 適用於nested route結構
2. useLocation 適用於沒使用nested route結構



### 使用useRouteMatch：透過match.url或者match.path

```
const Quote = () => {
  const params = useParams();
  const match = useRouteMatch();

  const quote = DUMMY_QUOTES.find((quote) => quote.id === params.quoteId);
  if (!quote) {
    return <p>No Quote Found!!</p>;
  }

  return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <HighLightedQuote text={quote.text} author={quote.author} />
      <Route path={`${match.path}`} exact>
        <div className='centered'>
          <Link to={`${match.url}/comments`} className='btn--flat'>
            Loads Comments
          </Link>
        </div>
      </Route>
      <Route path={`${match.path}/comments`}>
        <Comments />
      </Route>
    </React.Fragment>
  );
};
```


### 使用useLocation的案例：透過loaction.pathname
```
  const history = useHistory();
  const location = useLocation();

  const searchParams = new URLSearchParams(location.search);
  const isAscendingOrder = searchParams.get('sort') === 'asc';
  const resultQuotes = sortQuotes(props.quotes, isAscendingOrder);

  const sortClickHandler = () => {
    history.push(
      `${location.pathname}` +
        '?sort=' +
        `${isAscendingOrder ? 'desc' : 'asc'}`,
    );
  };
```

## 複習


Route 的path 寫法：盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑。

#🧠 react-router-dom：Route 會設定的path ，其寫法會是什麼？(寫不寫死)->->-> `盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑`

#🧠 react-router-dom：Route 會設定的path ，其寫法會是什麼？->->-> `盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑`


#🧠 react-router-dom：Route 會設定的path ，其寫法會是盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑，具體有何種實現概念？ ->->-> `使用useRouteMatch 從目前對應的parent route元件中取得路徑和實際路徑、使用useLocation 從目前頁面中取得實際路徑`


#🧠 react-router-dom：Route 會設定的path ，其寫法會是盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑，具體有何種實現概念？ 使用useRouteMatch 會是實現方向，那麼具體是利用他的什麼來取得什麼？  ->->-> `使用useRouteMatch 從目前對應的parent route元件中取得路徑和實際路徑`

#🧠 react-router-dom：Route 會設定的path ，其寫法會是盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑，具體有何種實現概念？ 使用useLocation 會是實現方向，那麼具體是利用他的什麼來取得什麼？  ->->-> `目前頁面中取得實際路徑`


#🧠 使用useRouteMatch 和 使用useLocation 的場景各是什麼？   ->->-> `useRouteMatch 適用於nested route結構、useLocation 適用於沒使用nested route結構`

#🧠 Question :: ->->-> ``



---
Status: #🌱 
Tags:
[[React]]
Links:
[[useRouteMatch是由react-router-dom所提供的hook，主要回傳一個route match object，其object會是夾雜目前元件所處的Route元件 A資訊和目前實際對應該元件A的URL資訊]]
References: