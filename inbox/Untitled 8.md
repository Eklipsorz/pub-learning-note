## 描述


nested Route 的path 盡量不將固定的路徑寫死，而是依照執行時資訊來決定其路徑

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


---
Status: #🌱 
Tags:
[[React]]
Links:
[[useRouteMatch是由react-router-dom所提供的hook，主要回傳一個route match object，其object會是夾雜目前元件所處的Route元件 A資訊和目前實際對應該元件A的URL資訊]]
References: