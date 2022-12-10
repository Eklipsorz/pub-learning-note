
## 描述



### 增加Quote的業務邏輯
主要實現：
1. 客戶端向後端發送增加Quote的請求
2. 客戶端獲取回應並於渲染之後，若增加成功就將使用者導向至\/quotes頁面
3. 渲染層面必須要根據請求是否處理中而顯示資料載入狀況


### 客戶端向後端發送增加Quote的請求

利用自製hook所得到的後端請求API來綁定Quote增加表格的提交事件，其後端請求主要是向後端耀求新增使用者輸入的Quote資訊至後端所管理的資料庫。

```
const { sendRequest, status } = useHttp(addQuote);

const addQuoteHandler = (data) => {
	sendRequest(data);
};

return <QuoteForm isLoading={status} onAddQuote={addQuoteHandler} />;
```

### 客戶端獲取回應並於渲染之後，若增加成功就將使用者導向至\/quotes頁面

指定useEffect來根據請求回應狀態是否為completed，若是的話，就導向；若不是的話，就不導向。

```
  useEffect(() => {
    if (status === 'completed') {
      history.push('/quotes');
    }
  }, [status, history]);
```

### 渲染層面必須要根據請求是否處理中而顯示資料載入狀況

將狀態請求回應狀態導入至QuoteForm的props屬性來讓該表格顯示。

```
 const { sendRequest, status } = useHttp(addQuote);
 .
 .
 .
 return <QuoteForm isLoading={status} onAddQuote={addQuoteHandler} />;
```


#### 完整代碼

```
import { useEffect } from 'react';
import { useHistory } from 'react-router-dom';

import QuoteForm from '../components/quotes/QuoteForm';
import useHttp from '../hooks/use-http';
import { addQuote } from '../lib/api';

const NewQuote = () => {
  const history = useHistory();

  const { sendRequest, status } = useHttp(addQuote);

  useEffect(() => {
    if (status === 'completed') {
      history.push('/quotes');
    }
  }, [status, history]);

  const addQuoteHandler = (data) => {
    sendRequest(data);
  };

  return <QuoteForm isLoading={status} onAddQuote={addQuoteHandler} />;
};

export default NewQuote;
```

## 複習

#🧠 若要實現增加Quote的業務邏輯，主要思路會有什麼？ ->->-> `1. 客戶端向後端發送增加Quote的請求 2. 客戶端獲取回應並於渲染之後，若增加成功就將使用者導向至\/quotes頁面 3. 渲染層面必須要根據請求是否處理中而顯示資料載入狀況`
<!--SR:!2022-12-14,4,230-->

#💻 請到/githubRepo/react-builder/question-review/react-router-question領取題目並切換至build-add-quote分支，在那請使用useHttp和lib/api.js來在NewQuote頁面調用相關API來要求後端增加指定資料至後端資料庫，成功完成請求後請從NewQuote頁面導向至Quotes頁面 ->->-> `https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/20-sending-getting-quote-data/src/pages/NewQuote.js`
<!--SR:!2023-01-03,26,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[react 前端優化方向可以從元件上的渲染層面和業務邏輯層面抽離出向後端發出的請求業務邏輯，並存放至src目錄下的lib目錄]]
References: