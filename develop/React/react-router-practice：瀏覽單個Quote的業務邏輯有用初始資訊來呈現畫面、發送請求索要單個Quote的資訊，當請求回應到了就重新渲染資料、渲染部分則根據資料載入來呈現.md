## 描述




### 瀏覽單個Quote的業務邏輯
主要實現：
1.  用初始資訊來呈現畫面，在這裡使用pending這狀態來表現載入中
2. 發送請求索要單個Quote的資訊，當請求回應到了就重新渲染資料
3. 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。



#### 完整代碼

```
import React, { useEffect } from 'react';
import { useParams, Route, Link, useRouteMatch } from 'react-router-dom';

import useHttp from '../hooks/use-http';
import { getSingleQuote } from '../lib/api';

import Comments from '../components/comments/Comments';
import HighLightedQuote from '../components/quotes/HighlightedQuote';
import NoQuotesFound from '../components/quotes/NoQuotesFound';
import LoadingSpinner from '../components/UI/LoadingSpinner';

const Quote = () => {
  const params = useParams();
  const match = useRouteMatch();
  const {
    sendRequest,
    status,
    data: loadedQuote,
    error,
  } = useHttp(getSingleQuote, true);

  const { quoteId } = params;

  useEffect(() => {
    sendRequest(quoteId);
  }, [sendRequest, quoteId]);

  if (status === 'pending') {
    return (
      <div className='centered'>
        <LoadingSpinner />
      </div>
    );
  }

  if (error) {
    return <p className='centered focused'>{error}</p>;
  }

  if (status === 'completed' && !loadedQuote.text && !loadedQuote.author) {
    return <NoQuotesFound />;
  }

  return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <HighLightedQuote text={loadedQuote.text} author={loadedQuote.author} />
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
export default Quote;																											
```

## 複習


#🧠 瀏覽單個Quote的業務邏輯，主要實現思路有哪些？ ->->-> `1.  用初始資訊來呈現畫面，在這裡使用pending這狀態來表現載入中 2. 發送請求索要單個Quote的資訊，當請求回應到了就重新渲染資料 3. 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。`
<!--SR:!2023-09-06,176,250-->

#💻 請到/githubRepo/react-builder/question-review/react-router-question 領取題目並切換至build-get-single-quote 分支，在那請使用useHttp和lib/api.js來在Quote.js實現瀏覽單個Quote功能，請務必要有辦法顯示找不到對應Quote、找到Quote、載入中的畫面->->-> `https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/20-sending-getting-quote-data/src/pages/QuoteDetail.js`
<!--SR:!2023-03-18,71,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[前端開發：在必須得擁有請求回應才能渲染真正的畫面 場景下，若採用先渲染後發送請求，會有以下做法。可先呈現初始資料或者載入中，後以請求回應來呈現]]
[[react-router-practice：呈現所有Quote的業務邏輯會需要用初始資訊來呈現畫面、 發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分、渲染部分則根據資料載入、錯誤來呈現狀況和載入]]
References: