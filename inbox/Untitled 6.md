## 描述

### 當使用者存取不存在資料的頁面時

當使用者存取不存在資料的頁面時，系統會提示使用者該頁面不存在或者404畫面

### * 在react-router上的Route元件之path用途為

[[@react-routerReactRouterDeclarativea]]

> path: string | string[]
> Any valid URL path or array of paths that path-to-regexp@^1.7.0 understands.


[[@path-to-regexpPillarjsPathtoregexpV1]]
> #### Asterisk *
> An asterisk can be used for matching everything.

\* 表示用來攔截任意長度的任意內容，在這裡會是將所有任意URL指定渲染為Component1

```
<Route path='*'>
	<Component1 />
</Route>
```

#### 實現404網頁


1. 呈現404頁面
```
const NotFound = () => {
  return (
    <div className='centered'>
      <p>Page not found!</p>
    </div>
  );
};

export default NotFound;
```

2. 將接收任意內容的path設定在最後一個，若使用者輸入合法的URL肯定會在前面渲染而不渲染到最後，除非真的找不到才會到最後一個
```
import { Switch, Route, Redirect } from 'react-router-dom';

import Quotes from './pages/Quotes';
import Quote from './pages/Quote';
import NewQuote from './pages/NewQuote';

import NotFound from './pages/NotFound';
import Layout from './components/layout/Layout';

function App() {
  return (
    <Layout>
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
        <Route path='*'>
          <NotFound />
        </Route>
      </Switch>
    </Layout>
  );
}

export default App;
```



## 複習



---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]
[[@path-to-regexpPillarjsPathtoregexpV1]]