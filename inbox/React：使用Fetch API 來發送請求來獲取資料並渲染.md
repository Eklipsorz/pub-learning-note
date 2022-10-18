
## 描述


### 前端發送請求的位置可以是
- 事件處理
- useEffect


### 瀏覽器向伺服器發送請求方式的工具

1. axios：瀏覽器本身不會內建，需載入額外模組才能使用
2. Fetch API ：瀏覽器內建工具




### Fetch API 是什麼

[[@FetchAPIWeb]]
> The Fetch API provides an interface for fetching resources (including across the network).


重點：
- 瀏覽器內建的API，會提供一個介面來方便獲取資料
	- 包含發送請求方法、請求物件、回應物件等代表請求/回應資訊的物件
- 該API用來向特定伺服器發送獲取資料和傳送資料請求 
	- 實際上是可以傳送資料，只是常用於獲取資料
- 其API 會是以Promise為基本來生成非同步任務去向指定伺服器索要：
	- resolve：會以response 物件回傳
	- reject：會回傳錯誤資訊


### Fetch API  語法

[[@mdnFetchWebAPIs]]
>  The global fetch() method starts the process of fetching a resource from the network, returning a promise which is fulfilled once the response is available.

> The promise resolves to the Response object representing the response to your request. 
```
fetch(resource)
fetch(resource, options)
```

> `resource`
> This defines the resource that you wish to fetch. 

> `options` Optional
>An object containing any custom settings that you want to apply to the request

重點：
- fetch(a, b) 為向指定伺服器獲取資料的方法，主要產生promise為主的非同步任務來做發送請求&接收回應
- 語法為：
	- 參數a：字串，定義要發送的伺服器是哪
	- 參數b：物件，設定請求封包，如HTTP請求方法(預設是GET)、狀態碼、多增加header
	- 回傳會是promise：
		- resolve：會以response 物件回傳
		- reject：會回傳錯誤資訊
```
fetch(a, b)
```

#### Fetch API vs. fetch()
1. Fetch API 是一個專門獲取資料的API，裡頭包含實際能獲取資料的方法、代表請求資訊的request object、代表回應資料的response object
2. fetch() 只是Fetch API內的其中一個方法

### response object


response 物件本身代表著回應封包

#### response.json()


[[@mdnResponseJsonWeb]]
>  The json() method of the Response interface takes a Response stream and reads it to completion. It returns a promise which resolves with the result of parsing the body text as JSON.


重點：
- json 方法 ：
	- 本身會是promise，主要會產生promise非同步任務來將body內容進行轉換
		- resolve：解析後的內容
		- reject：失敗
	- 讀取回應封包的body，並且將json格式轉換成javascript 的object 
	
### 案例1：promise

```
function App() {
  const [movies, setMovies] = useState([]);

  const fetchDataHandler = () => {
    fetch('https://swapi.dev/api/films')
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        const transformMovies = data.results.map((movie) => {
          return {
            id: movie.episode_id,
            title: movie.title,
            releaseDate: movie.release_date,
            openingText: movie.opening_crawl,
          };
        });
        setMovies(transformMovies)
      });
  };
  
  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>
        <MoviesList movies={movies} />
      </section>
    </React.Fragment>
  );
}
```

使用fetch 回應的電影資料來做渲染，具體需要：
- setState：當獲取到資料就以那份資料直接渲染
- 事件綁定/useEffect 來設定哪邊開始執行索要資料和setState

#### 案例1：改用async/await來寫


```
function App() {
  const [movies, setMovies] = useState([]);
  const fetchDataHandler = async () => {
    const response = await fetch('https://swapi.dev/api/films');
    const data = await response.json();

    const transformedMovies = data.results.map((movie) => ({
      id: movie.episode_id,
      title: movie.title,
      releaseDate: movie.release_date,
      openingText: movie.opening_crawl,
    }));

    setMovies(transformedMovies);
  };

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchDataHandler}>Fetch Movies</button>
      </section>
      <section>
        <MoviesList movies={movies} />
      </section>
    </React.Fragment>
  );
}
```

### fetch 命名緣由

[[@christineliddleWhatAreUsage]]
> Get (verb) = (got, getting) to obtain or receive. “She got first prize.” To become “Don’t get angry.” To reach a place “We got there by midnight.” To put or move “I can’t get my shoe one.” To prepare “Will you get the tea?”

> Bring (verb) = (brought, bringing) cause a person or thing to come, carry. “Bring the washing in from the line please.” “I’ll bring the nurse with me.”

> Fetch (verb) = go for and bring back. “Fetch some milk.” “Fetch the doctor.” To be sold for a particular price. “The chairs fetched $20.”

重點：
- get 單純意思為 **獲取** 或者 **接收**
- bring 單純意思為 **使某人事物過來**
- fetch 單純意思為 **去某個地方並從那帶回某個人事物** ，與get不同的是fetch包含 go 和 get 這意思。

## 複習

#🧠 get 單純意思為何？ ->->-> `**獲取** 或者 **接收**`
<!--SR:!2022-10-20,3,250-->

#🧠 bring 單純意思為？ ->->-> ` **使某人事物過來**`
<!--SR:!2022-10-20,3,250-->

#🧠 fetch 單純意思為？ ->->-> `**去某個地方並從那帶回某個人事物**`
<!--SR:!2022-10-20,3,250-->

#🧠 fetch vs. get 有差別嗎？有的話就說明->->-> `有，與get不同的是fetch包含 go 和 get 這意思`
<!--SR:!2022-10-20,3,250-->

#💻 請至/react-builder/question-review/http-req-practice領取題目，並切換成fetch-api-practice 這分支，請修改以Fetch API來獲取電影資料，API 文件為https://swapi.dev/documentation#films ->->-> `https://github.com/academind/react-complete-guide-code/blob/14-sending-http-requests/code/02-sending-a-get-request/src/App.js`
<!--SR:!2022-10-20,3,250-->


#💻 請至/react-builder/question-review/http-req-practice領取題目，並切換成async\/await-fetch-api-practice 這分支，請修改以async/await和Fetch API來獲取電影資料，API 文件為https://swapi.dev/documentation#films ->->-> `https://github.com/academind/react-complete-guide-code/blob/14-sending-http-requests/code/02-sending-a-get-request/src/App.js`->->-> ``
<!--SR:!2022-10-21,3,250-->

#🧠 瀏覽器向伺服器發送請求方式的工具有哪些？ ->->-> `axios、Fetch API`

#🧠 如何在瀏覽器使用axios 工具 ->->-> `瀏覽器本身並沒有，需要載入額外模組才能使用`

#🧠 如何在瀏覽器使用Fetch API工具 ->->-> `瀏覽器內建API，可以直接調用`

#🧠 Fetch API是什麼？ ->->-> `瀏覽器內建的API，會提供一個介面來方便獲取資料`

#🧠  Fetch API 是瀏覽器內建的API，會提供一個介面來方便獲取資料，介面包含了什麼？->->-> `包含發送請求方法、請求物件、回應物件等代表請求/回應資訊的物件`

#🧠 Fetch API 是瀏覽器內建的API，會提供一個介面來方便獲取資料，用途是什麼？->->-> `向伺服器發送任意請求`

#🧠 Fetch API 是瀏覽器內建的API，會提供一個介面來方便獲取資料，那麼就只能發送獲取資料的請求？ ->->-> `並不是，還可以發送其他種類的請求，如POST`

#🧠 Fetch API 是瀏覽器內建的API，專門用來向伺服器發送請求，請問如何發送？(任務) ->->-> `以Promise為基本來生成非同步任務去向指定伺服器索要	- resolve：會以response 物件回傳 - reject：會回傳錯誤資訊`

#🧠 Fetch API 是瀏覽器內建的API，專門用來向伺服器發送請求，請問方法語法為？->->-> `fetch(a, b)`

#🧠 Fetch API 是瀏覽器內建的API，其中發送請求的方法為fetch(a, b)，請問a 和 b各為什麼？->->-> `- 參數a：字串，定義要發送的伺服器是哪 - 參數b：物件，設定請求封包，如HTTP請求方法(預設是GET)、狀態碼、多增加header`

#🧠 Fetch API 是瀏覽器內建的API，其中發送請求的方法為fetch(a, b)，該方法主要會如何做發送請求&接收回應 ->->-> `主要產生promise為主的非同步任務來做發送請求&接收回應`

#🧠 Fetch API中的response object 是什麼？ ->->-> `response 物件本身代表著回應封包`


#🧠 Fetch API中的request object 是什麼？->->-> `表示請求封包`

#🧠 Fetch API中的fetch方法要如何處理JSON格式的回應封包 ->->-> `針對回應的response object來使用底下的json方法來解析和轉換`

#🧠 Fetch API 是瀏覽器內建的API，其中發送請求的方法為fetch(a, b)，b設定為請求封包 ，具體會是？->->-> `HTTP請求方法(預設是GET)、狀態碼、多增加header`


#🧠 Fetch API 和 fetch() 差別為何？->->-> `1. Fetch API 是一個專門獲取資料的API，裡頭包含實際能獲取資料的方法、代表請求資訊的request object、代表回應資料的response object 2. fetch() 只是Fetch API內的其中一個方法`


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@mdnFetchWebAPIs]]
[[@FetchAPIWeb]]
[[@mdnResponseJsonWeb]]
[[@christineliddleWhatAreUsage]]