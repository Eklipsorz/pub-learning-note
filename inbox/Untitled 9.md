
## 描述


### 替/quotes/:quoteId 增加 comments 這子路徑

在這裡會使用nested route安裝至路徑之下
```
/quotes/:quoteId
```

而要達到的目標會是
```
/quotes/:quoteId/comments
```


Quote.js 元件
```
import React from 'react';
import { useParams, Route } from 'react-router-dom';
import Comments from '../components/comments/Comments';

const Quote = () => {
  const params = useParams();

  return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <p>{params.quoteId}</p>
      <Route path={`/quotes/${params.quoteId}/comments`}>
        <Comments />
      </Route>
    </React.Fragment>
  );
};
```

## 複習


---
Status: 
Tags:
Links:
References: