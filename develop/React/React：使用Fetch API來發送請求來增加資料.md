
## 描述

### firebase realtime DB
- 會是以json檔案來當作資料庫來儲存，資料庫為NoSQL類別
- 提供一個簡易REST API介面來幫助開發者對特定資料庫進行CRUD
- 由於資料庫是json檔案為主，若轉換成JS的物件，就是一個物件來儲存內容，其屬性名稱為每一個項目的ID、屬性值則是該項目的實際內容



### content-type
[[@mdnContentTypeHTTPMDN]]
> The `**Content-Type**` representation header is used to indicate the original media type of the resource (prior to any content encoding applied for sending).

> In responses, a `Content-Type` header provides the client with the actual content type of the returned content

> In requests, (such as POST or PUT), the client tells the server what type of data is actually sent.

重點：
- 用途：
	-  告知目前封包裡的內容會是什麼格式，好讓接收者解析
	- 可以讓客戶端得知回應封包的內容格式，好讓客戶端方便解析
	- 可以讓伺服器得知請求封包的內容格式，好讓伺服器方便解析


### Fetch API 實現POST

fetch(URL, option) 實現POST會需要更改的option屬性：
- method：指定為 'POST'
- body： 指定要增加的資料，在這裡會是一個JSON 字串格式的資料
- headers：請求封包的header部分，在這裡會設定Content-Type為application/json

#### 實現

GET 
```
const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch(
        'https://xxxxxx/movies.json',
      );
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();
      const transformedMovies = [];

      for (let key in data) {
        transformedMovies.push({
          id: key,
          title: data[key].title,
          openingText: data[key].openingText,
          release: data[key].releaseDate,
        });
      }

      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }, []);

  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);
```

POST
```
  async function addMovieHandler(movie) {
    const response = await fetch(
      'https://xxxxxx/movies.json',
      {
        method: 'POST',
        body: JSON.stringify(movie),
        headers: {
          'Content-Type': 'application/json',
        },
      },
    );

    const data = response.json();
  }
```

## 複習



#🧠 封包中的content-type 主要是什麼？用途？->->-> `告知目前封包裡的內容會是什麼格式`
<!--SR:!2023-11-28,93,230-->

#🧠 當接收者沒看到封包裡有content-type，會衍生出什麼？->->-> `具體來說，接收者可能會採用預設方式來解析，這也有可能會使資料解析錯誤`
<!--SR:!2023-08-21,192,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API來發送請求- 只要頁面載入後就向伺服器發送請求來索要資料並渲染]]
[[React：使用Fetch API 來發送請求，且於獲取資料過程中發生錯誤所需要呈現的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染所需要的載入效果以及沒載入但卻沒資料時的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References:
[[@mdnContentTypeHTTPMDN]]