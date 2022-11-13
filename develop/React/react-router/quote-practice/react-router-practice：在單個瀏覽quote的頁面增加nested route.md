
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


#💻 請至/react-builder/question-review/react-router-question領取題目，切換至build-medium-routes分支，並建立瀏覽所有quotes、瀏覽單個quote、新增單個quote這三個頁面/服務的routing，除此之外還要當使用者瀏覽\/必須導向至瀏覽所有quotes以及讓瀏覽單個quote能夠擷取params資訊 ->->-> `https://github.com/academind/react-complete-guide-code/tree/20-building-mpas-with-react-router/code/11-practicing-nested-routes`
<!--SR:!2022-11-15,3,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router-practice：製作瀏覽單個quote、瀏覽所有quotes、建立新quote這三個頁面以及對應routing]]
[[react-router-practice：將根目錄導向quotes以及在單個瀏覽quote的頁面呈現params]]
References: