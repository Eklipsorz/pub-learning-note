## 描述


### 載入資料時發生錯誤
- 連線沒建立
- 連線建立但資料載入失敗 (401, 404, 500)


#### 狀態碼
2xx 狀態碼都代表著回應成功
4xx 狀態碼都代表伺服器成功接收且成功處理，但僅只是告知你沒辦法實現請求封包所要的
5xx 狀態碼都代表伺服器無法成功處理


### 載入時遇到錯誤時所會有的處理和渲染

- 先註冊狀態來表示是否有錯誤
`const [error, setError] = useState(null)`
- 在處理載入資料的程式模組前面添加重置錯誤的手段，**確保每一次畫面渲染都會按照是否正確來呈現**
```
setError(null)
// 處理載入資料
```
- 在處理載入資料的程式模組中的攔截錯誤部分添加，另外記得**添加setIsLoading(false)保證按照實際情況來呈現預期效果**
```
setError(error.message)
setIsLoading(false)
```

- 渲染部分則根據錯誤是否存在而呈現：
	- 由於發生錯誤時肯定會是以載入停止為前提，所以會是!isLoading && error作為條件
	- 其他條件是否會重疊而疊加，比如第二項若沒添加!error就會重疊
```
        {!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
        {!isLoading && !movies.length && !error && <p>Found No Data...</p>}
        {!isLoading && error && <p>{error}</p>}
        {isLoading && <p>Loading...</p>}
```
  

#### 整體實現
```
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchDataHandler = async () => {
    setError(null);
    setIsLoading(true);

    try {
      const response = await fetch('https://swapi.dev/api/film');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

      const transformedMovies = data.results.map((movie) => ({
        id: movie.episode_id,
        title: movie.title,
        releaseDate: movie.release_date,
        openingText: movie.opening_crawl,
      }));

      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  };

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>
        {!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
        {!isLoading && !movies.length && !error && <p>Found No Data...</p>}
        {!isLoading && error && <p>{error}</p>}
        {isLoading && <p>Loading...</p>}
      </section>
    </React.Fragment>
  );
}

export default App;

```

#### 整體實現：從渲染部分抽離出判斷業務邏輯

```
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchDataHandler = async () => {
    setError(null);
    setIsLoading(true);

    try {
      const response = await fetch('https://swapi.dev/api/films');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

      const transformedMovies = data.results.map((movie) => ({
        id: movie.episode_id,
        title: movie.title,
        releaseDate: movie.release_date,
        openingText: movie.opening_crawl,
      }));

      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  };

  let content = <p>Found No Data...</p>;

  if (movies.length > 0) {
    content = <MoviesList movies={movies} />;
  }
  if (error) {
    content = <p>{error}</p>;
  }

  if (isLoading) {
    content = <p>Loading...</p>;
  }

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>{content}</section>
    </React.Fragment>
  );
}
```

##### 細節

1. 如果載入中遇到錯誤的話，就應該會將狀態：
	- isLoading: true -> false (設定是為了避免預期外的錯誤)
	- error: false -> true
2. 要正式處理回應封包的內容前要先確保無錯誤
```
      const response = await fetch('https://swapi.dev/api/films');
      if (!response.ok) {
        setError('Something went wrong!');
      }

      const data = await response.json();
```

### 向伺服器發送請求的API是否會把夾雜錯誤狀態碼的回應物件視為真正的錯誤
  

> one problem we'll face here is that the Fetch API doesn't treat error status codes as real errors

- Fetch API 並不會把夾雜錯誤狀態碼的回應物件視為真正的錯誤
- axios API 會把夾雜錯誤狀態碼的回應物件視為真正的錯誤


#### 解法：
- 在try block中添加判斷狀態碼是否為錯誤代碼而手動拋錯
```
if (!response.ok) {
 throw new Error(...)
}
```

### Fetch API的回應物件response 對於狀態的屬性
Fetch API的回應物件response 會夾雜著狀態碼屬性：
- ok屬性，若狀態碼為2xx系列則會是true；若不是就會是false
- status 屬性，呈現回應封包的狀態碼

## 複習

要添加如何製作載入錯誤時所要有的畫面

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求來獲取資料並渲染所需要的載入效果以及沒載入但卻沒資料時的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References: