
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
	- 包含獲取方法、請求物件、回應物件等代表請求/回應資訊的物件
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
- fetch(a, b) 為向指定伺服器獲取資料的方法，主要產生promise為主的非同步任務來做連接獲取
- 語法為：
	- 參數a：字串，定義要發送的伺服器是哪
	- 參數b：物件，設定請求封包的資訊，如HTTP請求方法(預設是GET)、狀態碼、多增加header
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
	
### 案例

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

#🧠 bring 單純意思為？ ->->-> ` **使某人事物過來**`

#🧠 fetch 單純意思為？ ->->-> `**去某個地方並從那帶回某個人事物**`

#🧠 fetch vs. get 有差別嗎？有的話就說明->->-> `有，與get不同的是fetch包含 go 和 get 這意思`

#💻 請至/react-builder/question-review/http-req-practice領取題目，並切換成fetch-api-practice 這分支，請修改以Fetch API來獲取電影資料，API 文件為https://swapi.dev/documentation#films ->->-> `https://github.com/academind/react-complete-guide-code/blob/14-sending-http-requests/code/02-sending-a-get-request/src/App.js`



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