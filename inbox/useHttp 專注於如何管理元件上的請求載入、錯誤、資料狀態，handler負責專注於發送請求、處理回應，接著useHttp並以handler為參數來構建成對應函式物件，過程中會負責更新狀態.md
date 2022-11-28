

## 描述


useHttp 專注於如何管理元件上的請求載入、錯誤、資料狀態，handler負責專注於發送請求、處理回應，接著useHttp並以handler為參數來構建成對應函式物件，過程中會負責更新載入、錯誤、資料本身狀態。

### useHttp 內容
主要是負責：
1. 管理元件的請求載入、錯誤、資料狀態
2. 以handler為主來建立函式物件，其參數為handler所需要的資料，內容會負責更新載入、錯誤、資料本身狀態。
3. 回傳資料狀態、函式物件

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

#🧠 useHttp 若會是夾雜發送請求的API以及管理元件上的請求載入、錯誤、資料狀態，還能如何優化 ->->-> `useHttp 專注於如何管理元件上的請求載入、錯誤、資料狀態，handler負責專注於發送請求、處理回應，接著useHttp並以handler為參數來構建成對應函式物件來負責發送請求，過程中會負責更新載入、錯誤、資料本身狀態。`

#🧠 若useHttp 專注於如何管理元件上的請求載入、錯誤、資料狀態，並以handler為參數來構建成對應函式物件來負責發送請求，過程中會負責更新載入、錯誤、資料本身狀態。那麼useHttp 內容主要會是負責什麼？ ->->-> `1. 管理元件的請求載入、錯誤、資料狀態 2. 以handler為主來建立函式物件，其參數為handler所需要的資料，內容會負責更新載入、錯誤、資料本身狀態。 3. 回傳資料狀態、函式物件`

#🧠 若useHttp 專注於如何管理元件上的請求載入、錯誤、資料狀態，並以handler為參數來構建成對應函式物件來負責發送請求，過程中會負責更新載入、錯誤、資料本身狀態。handler內容主要會是負責什麼？ ->->-> `1. 向伺服器發送索要/處理資料的請求 2. 獲取請求回應並作處理，處理的回傳內容為空或者處理結果`


---
Status: #🌱 
Tags:
[[React]]
Links:
References: