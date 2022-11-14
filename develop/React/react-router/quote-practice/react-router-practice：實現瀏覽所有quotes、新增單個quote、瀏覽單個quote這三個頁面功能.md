## 描述



### 瀏覽所有quotes的頁面實作

```
import QuoteList from '../components/quotes/QuoteList';
import DUMMY_QUOTES from '../dummy-data';

const Quotes = () => {
  // display each quote
  return <QuoteList quotes={DUMMY_QUOTES} />;
};

export default Quotes;
```



### 新增單個quote的頁面實作

```
import QuoteForm from '../components/quotes/QuoteForm';

const NewQuote = () => {
  const addQuote = (data) => {
    console.log('addQuote', data);
  };
  // display a form for adding a quote
  return <QuoteForm onAddQuote={addQuote} />;
};

export default NewQuote;
```

### 瀏覽單個quote的頁面實作

```
import React from 'react';
import { useParams, Route } from 'react-router-dom';
import Comments from '../components/comments/Comments';
import HighLightedQuote from '../components/quotes/HighlightedQuote';
import DUMMY_QUOTES from '../dummy-data';

const Quote = () => {
  const params = useParams();

  const quote = DUMMY_QUOTES.find((quote) => quote.id === params.quoteId);
  if (!quote) {
    return <p>No Quote Found!!</p>;
  }

  return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <p>{params.quoteId}</p>
      <HighLightedQuote text={quote.text} author={quote.author} />
      <Route path={`/quotes/${params.quoteId}/comments`}>
        <Comments />
      </Route>
    </React.Fragment>
  );
};

export default Quote;
```


## 複習

#💻 請至/react-builder/question-review/react-router-question領取題目並切換成implement-all-pages這個分支，請實現瀏覽所有quote的頁面、瀏覽單個quote的頁面、新增單個quote的頁面，其中第一個會用到QuoteList現成元件、第二個則是會用到HighLightedQuote現成元件(注意若沒有對應quoteId就顯示沒東西)、第三個則是會用到QuoteForm這現成元件，quote資料放在dummy-data.js那 ->->-> `https://github.com/academind/react-complete-guide-code/tree/20-building-mpas-with-react-router/code/13-adding-dummy-data-and-more-content/src/pages`
<!--SR:!2022-11-17,3,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
References: