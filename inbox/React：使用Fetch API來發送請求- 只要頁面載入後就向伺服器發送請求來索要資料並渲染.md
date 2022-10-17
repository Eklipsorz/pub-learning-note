
## 描述


### 假若要實現-只要頁面載入後就向伺服器發送請求來索要資料並渲染

會使用：
- useEffect 會以fetchDataHandler為deps
- useCallback 

在這裡為了讓useEffect 裡頭的callback變複雜，而將主要的業務邏輯分離至外面的函式-fetchDataHandler，並設定useEffect的deps為該fetchDataHandler，避免變動。

```
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

  useEffect(() => {
    fetchDataHandler();
  }, [fetchDataHandler]);
```


但由於fetchDataHandler 本身是物件，會因為component function的執行而一直產生出新的fetchDataHandler物件，致使useEffect會因為deps設定為fetchDataHandler而陷入無限循環的問題，為此會使用useCallback來儲存剛載入所有元件後的fetchDataHandler物件作為主要內容


之後每一次的component function 執行，只會回傳那個時期的fetchDataHandler物件，這也使得useEffect只會執行一次，也就是剛載入所有元件後就執行的那一次

```
  const fetchDataHandler = useCallback(async () => {
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
  }, []);

  useEffect(() => {
    fetchDataHandler();
  }, [fetchDataHandler]);
```

#### 實現

```
import React, { useState, useCallback, useEffect } from 'react';

import MoviesList from './components/MoviesList';
import './App.css';

function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchDataHandler = useCallback(async () => {
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
  }, []);

  useEffect(() => {
    fetchDataHandler();
  }, [fetchDataHandler]);

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

export default App;

```

### useEffect 最佳實踐

>  to list all deps you use instead of the effect function here in the dependencies array
>  

列出所有會在effect使用到的項目至useEffect 的依賴項目







## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求，且於獲取資料過程中發生錯誤所需要呈現的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染所需要的載入效果以及沒載入但卻沒資料時的額外呈現效果]]
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References: