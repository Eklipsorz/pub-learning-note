

## 描述


### useHttp 內容
主要是負責：
1. 管理元件的請求載入、錯誤、資料狀態
2. 以handler來建立函式物件
3. 

```
function useHttp(requestFunction, startWithPending = false) {
  const [httpState, dispatch] = useReducer(httpReducer, {
    status: startWithPending ? 'pending' : null,
    data: null,
    error: null,
  });

  const sendRequest = useCallback(
    async function (requestData) {
      dispatch({ type: 'SEND' });
      try {
        const responseData = await requestFunction(requestData);
        dispatch({ type: 'SUCCESS', responseData });
      } catch (error) {
        dispatch({
          type: 'ERROR',
          errorMessage: error.message || 'Something went wrong!',
        });
      }
    },
    [requestFunction],
  );

  return {
    sendRequest,
    ...httpState,
  };
}
```


### handler 內容

主要是負責：
1. 向伺服器發送索要/處理資料的請求
2. 獲取請求回應並作處理，處理的回傳內容為空或者處理結果

```
const FIREBASE_DOMAIN = XXXX;

export async function getAllQuotes() {
  ....
}

export async function getSingleQuote(quoteId) {
  ....
}
```

## 複習


---
Status: #🌱 
Tags:
Links:
References: