
## 描述


### 增加Quote的業務邏輯
主要實現：
1. 客戶端向後端發送增加Quote的請求
2. 客戶端獲取回應並於渲染之後，若增加成功就將使用者導向至\/quotes頁面
3. 渲染層面必須要根據請求是否處理中而


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

---
Status: #🌱 
Tags:
[[React]]
Links:
[[react 前端優化方向可以從元件上的渲染層面和業務邏輯層面抽離出向後端發出的請求業務邏輯，並存放至src目錄下的lib目錄]]
References: