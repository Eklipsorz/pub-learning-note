
## 描述


###  定義BrowserRouter 並安裝至Index.js來包含App.js元件
```
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
);
```

### 在App.js元件上定義BrowserRouter的Routing

```
import { Switch, Route } from 'react-router-dom';

import Quotes from './pages/Quotes';
import Quote from './pages/Quote';
import NewQuote from './pages/NewQuote';

function App() {
  return (
    <Switch>
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

export default App;
```


### 端點名稱

製作三個不同的pages：
1. 呈現所有quotes的頁面 
	- 頁面檔案：Quotes.js
	- 路徑：/quotes
2. 呈現單個quote的頁面 
	- 頁面檔案：Quote.js
	- 路徑：/quote
3. 新增單個quote的頁面 
	- 頁面檔案：NewQuote.js
	- 路徑：/new-quote

## 複習

#💻 請至/react-builder/question-review/react-router-question領取題目，切換至build-simple-routes分支，並建立瀏覽所有quotes、瀏覽單個quote、新增單個quote這三個頁面/服務的routing ->->-> `https://github.com/academind/react-complete-guide-code/tree/20-building-mpas-with-react-router/code/10-practice-redirecting-and-extracting-params/src`


---
Status: #🌱 
Tags:
[[React]]
Links:
[[RESTful API：端點命名法則通常會因為URI的域名限制而一律使用Spinal Case]]
References: