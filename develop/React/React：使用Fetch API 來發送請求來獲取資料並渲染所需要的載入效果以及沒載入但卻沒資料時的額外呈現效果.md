
## 描述


### 載入資料來渲染所需要注意的情況

根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料可以分為四種情況

1. 沒進行載入資料且沒初始渲染資料的情況：告知沒資料
2. 沒進行載入資料且有初始渲染資料的情況：以初始渲染資料來渲染畫面
3. 載入資料進行中且初始渲染資料為任意的情況：由於都處於載入進行中，只是需要告知載入中
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


#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，資料載入會分出什麼狀態？->->-> `根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料`
<!--SR:!2023-10-09,104,208-->
<!--SR:!2023-08-29,197,250-->

#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，資料載入會分出什麼狀態？->->-> `根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料`
<!--SR:!2023-10-09,104,208-->


#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，根據資料載入狀況和是否有初始渲染資料可以分為四種情況，請問資料載入狀況能分成什麼？ ->->-> `(沒進行、進行中、完成)`
<!--SR:!2023-09-18,195,230-->

#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，可以根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料分為哪四種狀況？ ->->-> `沒進行載入資料且沒初始渲染資料的情況、沒進行載入資料且有初始渲染資料的情況、載入資料進行中且初始渲染資料為任意的情況、載入資料完成且有初始資料渲染為任意的情況`
<!--SR:!2023-11-26,245,249-->

#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，可以根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料，請問面對沒進行載入資料且沒初始渲染資料的情況要如何增加使用者體驗->->-> `告知沒資料`
<!--SR:!2023-08-16,188,250-->

#🧠 React ：當使用Fetch API或者其他API來發送請求來獲取資料並渲染，其渲染畫面和資料載入的開發上，一開始會帶給使用者什麼樣潛在問題？ ->->-> `最主要是無法讓使用者得知目前資料載入狀況，會有載入並渲染的過程中，並沒有告知使用者以及沒資料也沒載入時，並沒有告知使用者目前沒資料`
<!--SR:!2023-10-10,99,190-->

#🧠 React ：當使用Fetch API 來發送請求來獲取資料並渲染，可以根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料，請問面對載入資料進行中且初始渲染資料為任意的情況要如何增加使用者體驗->->-> `由於都處於載入進行中，只是需要告知載入中`
<!--SR:!2023-11-29,94,230-->

#🧠 React ：當使用Fetch API 來發送請求來獲取資料並渲染，可以根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料，請問面對沒進行載入資料且有初始渲染資料的情況要如何增加使用者體驗->->-> `以初始渲染資料來渲染畫面`
<!--SR:!2024-09-05,415,250-->

#🧠 React ：當使用Fetch API或者其他API 來發送請求來獲取資料並渲染，可以根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料，請問面對 載入資料完成且有初始資料渲染為任意的情況要如何增加使用者體驗->->-> `由於都處於載入完成，所需要呈現渲染畫面就直接以獲取到的資料為主`
<!--SR:!2023-09-29,212,249-->


#🧠 React：當使用Fetch API 或者其他API來發送請求來獲取資料並渲染，要如何實現載入資料進行中且初始渲染資料為任意的情況下實現告知載入中 ->->-> `先在元件下註冊isLoading這狀態const [isLoading, setIsLoading] = useState(false);、然後在處理載入資料的程式模組前一行添加setState以及處理載入資料的程式模組後一行添加setState：1.  setIsLoading(true) 2.  // 載入資料處理 3.  setIsLoading(false)。最後，在渲染部分，根據isLoading是否為true來調整畫面，{!isLoading && <MoviesList movies={movies} />}{isLoading && <p>Loading...</p>}`
<!--SR:!2024-08-27,406,250-->

#🧠 React：當使用Fetch API 或者其他API 來發送請求來獲取資料並渲染，要如何實現沒載入資料進行中且沒初始渲染資料為任意的情況下實現告知沒資料？ ->->-> `在渲染部分，根據movies的資料數來判定是否沒初始資料(在這裡搭配上述的載入資料中情況)`
<!--SR:!2024-01-02,268,249-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References: