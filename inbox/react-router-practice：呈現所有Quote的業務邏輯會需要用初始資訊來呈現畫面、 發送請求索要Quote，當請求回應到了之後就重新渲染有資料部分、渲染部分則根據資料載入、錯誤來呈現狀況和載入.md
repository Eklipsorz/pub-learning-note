## 描述



### 呈現所有Quote的業務邏輯
主要實現：
1. 用初始資訊來呈現畫面，在這裡是使用pending這狀態來表現載入中
2. 發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分
3. 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。


### 用初始資訊來呈現畫面
在這裡是使用pending這狀態來表現載入中，最主要會直接以載入中來呈現

```
const {
	sendRequest,
    status,
    data: loadedQuotes,
    error,
} = useHttp(getAllQuotes, true);


if (status === 'pending') {
    return (
      <div className='centered'>
        <LoadingSpinner />
      </div>
	);
}

```

### 發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分

先用初始資料渲染一遍畫面之後，再向後端請求索要Quote，等到回應到了就重新渲染對應資料的部分

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

#🧠  若要實現呈現所有Quote的業務邏輯，主要思路會有什麼？->->-> `主要實現： 1. 用初始資訊來呈現畫面 2. 發送請求索要Quote，當請求回應到了之後就重新渲染有資料部分 3. 渲染部分則根據資料載入、錯誤來呈現狀況和載入到的資料。`
<!--SR:!2023-01-05,25,250-->

#💻 請到/githubRepo/react-builder/question-review/react-router-question領取題目並切換至build-get-all-quotes分支，在那請使用useHttp和lib/api.js來在Quotes頁面，調用相關API來要求後端獲取所有Quote資料，接著依據獲取狀況來印出初始資料、載入中、錯誤、載入後的資料呈現在畫面上 ->->-> `https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/20-sending-getting-quote-data/src/pages/AllQuotes.js`
<!--SR:!2023-01-07,28,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[前端開發：在必須得擁有請求回應才能渲染真正的畫面 場景下，若採用先渲染後發送請求，會有以下做法。可先呈現初始資料或者載入中，後以請求回應來呈現]]
References: