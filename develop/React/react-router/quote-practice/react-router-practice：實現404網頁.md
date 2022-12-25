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

#🧠 當使用者存取不存在資料的頁面時，通常處理方會做些什麼來增加使用者體驗->->-> `以404網頁來告知使用者網頁不存在`
<!--SR:!2023-02-04,51,250-->

#🧠 react-router-dom：\<Route path=\'\*\'\>\<Component1 \/\> \<\/Route\>中的*做什麼用？->->-> `表示用來攔截任意長度的任意內容，在這裡會是將所有任意URL指定渲染為Component1`
<!--SR:!2023-02-27,67,250-->

#💻 react-router-v5 請到githubRepo/react-builder/question-review/react-router-question領取題目並切換至build-not-found-page分支，請實現404網頁->->-> `https://github.com/academind/react-complete-guide-code/tree/20-building-mpas-with-react-router/code/15-adding-a-notfound-page/src`
<!--SR:!2023-03-09,74,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]
[[@path-to-regexpPillarjsPathtoregexpV1]]