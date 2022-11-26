## 描述


### 呈現所有Quote的業務邏輯
主要實現：
1. 用初始資訊來呈現畫面
2. 發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分
3. 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。


### 用初始資訊來呈現畫面
```
  const {
    sendRequest,
    status,
    data: loadedQuotes,
    error,
  } = useHttp(getAllQuotes, true);
```

### 先初始資訊來呈現畫面並之後發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分


```
  useEffect(() => {
    sendRequest();
  }, [sendRequest]);

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

  if (status === 'completed' && !loadedQuotes.length) {
    return <NoQuotesFound />;
  }

  if (!loadedQuotes) {
    return <NoQuotesFound />;
  }

  return <QuoteList quotes={loadedQuotes} />;
};
```


### 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。

```
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

  if (status === 'completed' && !loadedQuotes.length) {
    return <NoQuotesFound />;
  }

  if (!loadedQuotes) {
    return <NoQuotesFound />;
  }

  return <QuoteList quotes={loadedQuotes} />;
};

```


#### 完整代碼

```
import { useEffect } from 'react';

import useHttp from '../hooks/use-http';
import { getAllQuotes } from '../lib/api';

import NoQuotesFound from '../components/quotes/NoQuotesFound';
import LoadingSpinner from '../components/UI/LoadingSpinner';
import QuoteList from '../components/quotes/QuoteList';

const Quotes = () => {
  const {
    sendRequest,
    status,
    data: loadedQuotes,
    error,
  } = useHttp(getAllQuotes, true);

  useEffect(() => {
    sendRequest();
  }, [sendRequest]);

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

  if (status === 'completed' && !loadedQuotes.length) {
    return <NoQuotesFound />;
  }

  if (!loadedQuotes) {
    return <NoQuotesFound />;
  }

  return <QuoteList quotes={loadedQuotes} />;
};

export default Quotes;
```


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: