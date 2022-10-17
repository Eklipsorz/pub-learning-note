
## 描述


### 載入資料來渲染所需要注意的情況

根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料可以分為四種情況

1. 沒進行載入資料且沒初始渲染資料的情況：告知沒資料
2. 沒進行載入資料且有初始渲染資料的情況：以初始渲染資料來渲染畫面
3. 載入資料進行中且初始渲染資料為任意的情況：由於都處於載入進行中，所需要呈現渲染畫面都會是載入效果。
4. 載入資料完成且有初始資料渲染為任意的情況：由於都處於載入完成，所需要呈現渲染畫面就直接以獲取到的資料為主


在這裡，第二和第四種情況可以根據是否有資料來呈現畫面，但第一和第三是較為特殊的情況，因此必須要有特定畫面來告知目前沒資料以及正在載入資料中這些訊息

目的是為了告知使用者目前狀態是什麼，好增加使用者體驗

### 載入資料進行中且初始渲染資料為任意的情況

若要呈現正在載入的文字，流程會是
1. 先在元件下註冊isLoading這狀態
`const [isLoading, setIsLoading] = useState(false);`

2. 然後在處理載入資料的程式模組前一行添加setState以及處理載入資料的程式模組後一行添加setState
```
1.  setIsLoading(true)
2.  // 載入資料處理
3.  setIsLoading(false)
```

3. 在渲染部分，根據isLoading是否為true來調整畫面
```
{!isLoading && <MoviesList movies={movies} />}
{isLoading && <p>Loading...</p>}
```


#### 整體程式碼

```
import React, { useState } from 'react';

import MoviesList from './components/MoviesList';
import './App.css';

function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);

  const fetchDataHandler = async () => {
    setIsLoading(true);
    const response = await fetch('https://swapi.dev/api/films');
    const data = await response.json();

    const transformedMovies = data.results.map((movie) => ({
      id: movie.episode_id,
      title: movie.title,
      releaseDate: movie.release_date,
      openingText: movie.opening_crawl,
    }));

    setMovies(transformedMovies);
    setIsLoading(false);
  };

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>
        {!isLoading && <MoviesList movies={movies} />}
        {isLoading && <p>Loading...</p>}
      </section>
    </React.Fragment>
  );
}

export default App;
```

### 沒進行載入資料且沒初始渲染資料的情況

1. 在渲染部分，根據movies的資料數來判定是否沒初始資料(在這裡搭配上述的載入資料中情況)
```
{!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
{!isLoading && !movies.length && <p>Found No Data...</p>}
{isLoading && <p>Loading...</p>}
```


#### 整體程式碼
```
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);

  const fetchDataHandler = async () => {
    setIsLoading(true);
    const response = await fetch('https://swapi.dev/api/films');
    const data = await response.json();

    const transformedMovies = data.results.map((movie) => ({
      id: movie.episode_id,
      title: movie.title,
      releaseDate: movie.release_date,
      openingText: movie.opening_crawl,
    }));

    setMovies(transformedMovies);
    setIsLoading(false);
  };

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>
        {!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
        {!isLoading && !movies.length && <p>Found No Data...</p>}
        {isLoading && <p>Loading...</p>}
      </section>
    </React.Fragment>
  );
}
```

## 複習

添加特殊狀況時所要有的畫面


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References: