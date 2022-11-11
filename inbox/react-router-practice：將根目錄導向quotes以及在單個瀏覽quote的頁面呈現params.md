## 描述


### 替/nothing 導向 /quotes

```
function App() {
  return (
    <Switch>
      <Route path='/' exact>
        <Redirect to='/quotes' />
      </Route>
      <Route path='/quotes' exact>
        <Quotes />
      </Route>
      <Route path='/quotes/:quoteId'>
        <Quote />
      </Route>
      <Route path='/new-quote'>
        <NewQuote />
      </Route>
    </Switch>
  );
}
```

### 替/quotes/:quoteId 顯示對應params

```
import React from 'react';
import { useParams } from 'react-router-dom';

const Quote = () => {
  const params = useParams();

  return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <p>{params.quoteId}</p>
    </React.Fragment>
  );
};

export default Quote;

```

## 複習



---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router-practice：製作瀏覽單個quote、瀏覽所有quotes、建立新quote這三個頁面以及對應routing]]
[[react-router-practice：在單個瀏覽quote的頁面增加nested route]]
References: