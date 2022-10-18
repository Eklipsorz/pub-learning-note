
## 描述

and i mentioned, even though it's called fetch, it's not just the air to fetch data, you can also use that same function to send data



由於firebase realtime db 回傳會是以一個物件來包含所有項目資料，其中每個屬性名稱會是資料項目的ID，而每個屬性值會是該資料項目的資料，所以得有個手段來枚舉

  

  

// 枚舉obj物件的每個屬性 並轉換成一個陣列  
for (var prop in obj) { }

  

// 以該陣列來觸發更新和渲染




firebase realtime DB 回應內容會是以JSON格式來回傳
Here for Firebase, sending a POST request. we'll create a resource
firebase 由於提供的資料庫是由MongoDB 系統所提供，該系統會以json檔案來當作一個資料庫來記錄資料



fetch(URL, option) 實現POST會需要更改的option屬性：

- method：指定為 'POST'

- body： 指定要增加的資料，在這裡會是一個JSON 字串格式的資料

- headers：請求封包的header部分，在這裡會設定Content-Type為application/json

  

Technically this header is not required by Firebase, it would be able to handle request even if that header is not set, but a lot of rest APIs to which you might be sending requests later, might require this extra header, which describes to content that will be sent

  

The `**Content-Type**` representation header is used to indicate the original media type of the resource (prior to any content encoding applied for sending).

-> Content-Type 告知對方傳送的resource會是什麼格式的


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

#💻 Question :: ->->-> ``


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