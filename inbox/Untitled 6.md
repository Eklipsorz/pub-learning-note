## 描述


```
import React, { useEffect } from 'react';
import { useParams, Route, Link, useRouteMatch } from 'react-router-dom';

import useHttp from '../hooks/use-http';
import { getSingleQuote } from '../lib/api';

import Comments from '../components/comments/Comments';
import HighLightedQuote from '../components/quotes/HighlightedQuote';
import NoQuotesFound from '../components/quotes/NoQuotesFound';
import LoadingSpinner from '../components/UI/LoadingSpinner';
// import DUMMY_QUOTES from '../dummy-data';

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
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: