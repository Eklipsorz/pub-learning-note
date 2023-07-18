## 描述


### 載入資料時發生錯誤
- 連線沒建立
- 連線建立但資料載入失敗 (401, 404, 500)


#### 狀態碼
[[@wikidataHTTPZhuangTaiMa2022]]
> 2xx
>這一類型的狀態碼，代表請求已成功被伺服器接收、理解、並接受


> 3xx
> 這類狀態碼代表需要客戶端採取進一步的操作才能完成請求。通常，這些狀態碼用來重新導向，後續的請求位址（重新導向目標）在本次回應的Location域中指明

> 4xx
> 這類的狀態碼代表了客戶端看起來可能發生了錯誤，妨礙了伺服器的處理

> 5xx
>表示伺服器無法完成明顯有效的請求。

2xx 狀態碼都代表著客戶端發送的請求處理成功
3xx 狀態碼都代表著告知客戶端需要採取進一步的操作才能完成請求，通常會是要求客戶端導向特定頁面
4xx 狀態碼都代表伺服器成功接收，但僅只是告知客戶端請求發生錯誤
5xx 狀態碼都代表伺服器無法成功處理


### 載入時遇到錯誤時所會有的處理和渲染

- 先註冊狀態來表示是否有錯誤
`const [error, setError] = useState(null)`
- 在處理載入資料的程式模組前面添加重置錯誤的手段，**確保每一次畫面渲染都會按照是否正確來呈現**
```
setError(null)
// 處理載入資料
```
- 在處理載入資料的程式模組中的攔截錯誤部分添加，另外記得**添加setIsLoading(false)保證按照按照實際情況來呈現預期效果**
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

#🧠 HTTP 狀態碼大致上可分為？ ->->-> `2xx系列、3xx系列、4xx系列、5xxx系列`
<!--SR:!2024-07-27,393,250-->

#🧠 HTTP 狀態碼：2xx系列狀態碼代表著什麼？ ->->-> `客戶端發送的請求處理成功`
<!--SR:!2023-08-18,189,250-->

#🧠 HTTP 狀態碼：3xx系列狀態碼代表著什麼？ ->->-> `告知客戶端需要採取進一步的操作才能完成請求，通常會是要求客戶端導向特定頁面`
<!--SR:!2024-08-26,411,250-->

#🧠 HTTP 狀態碼：3xx系列狀態碼代表告知客戶端需要採取進一步的操作才能完成請求，通常會是什麼？ ->->-> `要求客戶端導向特定頁面`
<!--SR:!2023-08-21,192,250-->

#🧠 HTTP 狀態碼：3xx系列狀態碼代表著什麼？ 3xx就可以說明伺服器本身有問題嗎？為什麼？->->-> `並不能說明，主要只是伺服器要求客戶端做些什麼才能完成`
<!--SR:!2023-08-07,183,250-->

#🧠 HTTP 狀態碼：4xx系列狀態碼代表著什麼？ ->->-> `伺服器成功接收且處理，但僅只是告知客戶端請求發生錯誤`
<!--SR:!2024-09-10,420,250-->

#🧠 HTTP 狀態碼：4xx系列狀態碼代表著什麼？ 4xx就可以說明伺服器本身有問題嗎？為什麼？->->-> `並不能說明，主要源自客戶端所給予的問題`
<!--SR:!2024-08-15,401,250-->

#🧠 HTTP 狀態碼：5xx系列狀態碼代表著什麼？->->-> `都代表伺服器無法成功處理`
<!--SR:!2023-08-17,189,250-->

#🧠 HTTP 狀態碼：哪些是主要的錯誤狀態碼 ->->-> `4xx、5xx系列狀態馬`
<!--SR:!2023-08-16,188,250-->

#🧠 請問瀏覽器發送請求的API 都能夠把夾雜錯誤狀態碼的回應封包當作是真正的錯誤嗎？->->-> `並不能，主要要看API的實現是如何？`
<!--SR:!2024-03-23,249,230-->

#🧠 請問瀏覽器發送請求的API是使用Fetch API的話，會把夾雜錯誤狀態碼的回應封包當作是真正的錯誤嗎？ ->->-> `並不會把夾雜錯誤狀態碼的回應物件視為真正的錯誤`
<!--SR:!2024-09-19,429,250-->


#🧠 請問瀏覽器發送請求的API是使用axios的話，會把夾雜錯誤狀態碼的回應封包當作是真正的錯誤嗎？ ->->-> `會把夾雜錯誤狀態碼的回應物件視為真正的錯誤`
<!--SR:!2023-06-18,148,250-->

#🧠 React：瀏覽器向伺服器發送請求來獲取資料並渲染時，期間若發生錯誤，該如何處理對應渲染？以程式碼來說 ->->-> `先註冊狀態來表示是否有錯誤：const [error, setError] = useState(null)。在處理載入資料的程式模組前面添加重置錯誤的手段，**確保每一次畫面渲染都會按照是否正確來呈現**： setError(null) // 處理載入資料。 在處理載入資料的程式模組中的攔截錯誤部分開頭添加，另外記得**添加setIsLoading(false)保證按照實際情況來呈現預期效果** 。渲染部分則根據錯誤是否存在而呈現`
<!--SR:!2023-04-24,24,210-->

#🧠 瀏覽器在處理向伺服器發送請求所遇到的錯誤時，所做的渲染處理若有：在處理載入資料的程式模組前面添加重置錯誤的手段：setError(null) \/\/ 處理載入資料，請問為什麼要添加->->-> `確保每一次畫面渲染都會按照是否正確來呈現`
<!--SR:!2024-09-06,416,250-->


#🧠 瀏覽器在處理向伺服器發送請求所遇到的錯誤時，所做的渲染處理若有：在處理載入資料的程式模組中的攔截錯誤部分添加setIsLoading(false)：setError(error.message) setIsLoading(false)，請問為什麼要添加 ->->-> `保證按照按照實際情況來呈現預期效果`
<!--SR:!2023-09-01,199,250-->

#🧠 若瀏覽器使用的API不會把夾雜錯誤狀態碼的回應物件視為真正的錯誤，那麼解法會是什麼？->->-> `根據回應封包結果來設定手動拋錯`
<!--SR:!2023-08-22,193,250-->

#🧠 Fetch API的回應物件response 會夾雜著狀態碼屬性，其中ok屬性是？ ->->-> ` ok屬性，若狀態碼為2xx系列則會是true；若不是就會是false`
<!--SR:!2024-09-01,417,250-->


#🧠 Fetch API的回應物件response 會夾雜著狀態碼屬性，其中status屬性是？->->-> `呈現回應封包的狀態碼`
<!--SR:!2024-08-26,408,250-->

#🧠 當在前端使用API向伺服器索要資料並獲取到資料進行處理前，要做什麼？ ->->-> `要正式處理回應封包的內容前要先確保無錯誤`
<!--SR:!2023-07-31,161,230-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求來獲取資料並渲染所需要的載入效果以及沒載入但卻沒資料時的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References:
[[@wikidataHTTPZhuangTaiMa2022]]