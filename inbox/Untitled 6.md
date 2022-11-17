## 描述



### Query string
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]

由於使用特定符號來區隔：一邊為伺服器端點；另一邊為query string，所以本身可以被任意特定路由處理器給攔截到。


### Query string 應用

應用：

1. 接收參數來對指定項目做排序


### Query string 應用：接收參數來對指定項目做排序之概念
製作排序清單項目的功能：
- 將排序邏輯部分分到資料業務邏輯那
- 再將處理後的資料放到渲染層面







1. 將使用者以programatic navigation 方式來從目前頁面轉移至其他頁面所在網址

    - 網址會是/quotes?sort=xxxx：添加query string的形式來重新對該端點發送請求，讓他們接收到參數來排序資料，然後再把資料放到渲染層面




### 實現渲染層面上的排序元件功能


渲染層面若要添加排序按鈕的話，可以為按鈕的點擊事件添加：
1. 將使用者以programatic navigation 方式來從目前頁面轉移至其他頁面所在網址
	- 網址會是/quotes?sort=xxxx：添加query string的形式來重新對該端點發送請求，讓他們接收到參數來排序資料，然後再把資料放到渲染層面

具體實現可以是以執行結果來決定排序方式，而非寫死，實現會是如下，其中sorting會是變數：
`'/quotes?sort=' + sorting`





```
import { Fragment } from 'react';
import { useHistory, useLocation } from 'react-router-dom';
import QuoteItem from './QuoteItem';
import classes from './QuoteList.module.css';

const sortQuotes = (quotes, ascending) => {
  return quotes.sort((quoteA, quoteB) => {
    if (ascending) {
      return quoteA.id > quoteB.id ? 1 : -1;
    } else {
      return quoteA.id < quoteB.id ? 1 : -1;
    }
  });
};

const QuoteList = (props) => {
  const history = useHistory();
  const location = useLocation();

  const searchParams = new URLSearchParams(location.search);
  const isAscendingOrder = searchParams.get('sort') === 'asc';
  const resultQuotes = sortQuotes(props.quotes, isAscendingOrder);

  const sortClickHandler = () => {
    history.push('/quotes?sort=' + (isAscendingOrder ? 'desc' : 'asc'));
  };

  return (
    <Fragment>
      <div className={classes.sorting}>
        <button onClick={sortClickHandler}>{`Sort ${
          isAscendingOrder ? 'Ascending' : 'Descending'
        }`}</button>
      </div>
      <ul className={classes.list}>
        {resultQuotes.map((quote) => (
          <QuoteItem
            key={quote.id}
            id={quote.id}
            author={quote.author}
            text={quote.text}
          />
        ))}
      </ul>
    </Fragment>
  );
};

export default QuoteList;
```











## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
[[QueryString 加號問題 - 伺服器在解析query參數時就會自動以無UTF8形式來解碼，其+被解出來會是空白]]
[[URLSearchParams 是內建於瀏覽器並以JS而撰寫的介面，專門協助開發者處理特定URL上的query string]]
[[useLocation會回傳location object，而該物件夾帶著目前載入的頁面所擁有的資訊(含URL部分)]]
[[react-router 所提供的 history.push & replace：若每一次對stack的最上面元素做push或replace，會針對切換前後的畫面之間差異來切換，而非單方面使react執行一次unmount 和 一次mount]]
References:
