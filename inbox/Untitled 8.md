
## 描述


### 瀏覽器向伺服器發送請求方式的工具

1. axios：瀏覽器本身不會內建，需載入額外模組才能使用
2. fetch：瀏覽器內建工具




### fetch API 是什麼

[[@FetchAPIWeb]]
> The Fetch API provides an interface for fetching resources (including across the network).


- 瀏覽器內建API

- 該API用來向後端發送獲取資料和傳送資料請求 (it allows us to fetch data and actually also to send data)


前端發送請求的位置可以是：

- 事件處理

- useEffect



### fetch API 語法

fetch(a, b) 參數說明：

- 參數a：字串，定義要發送的端點是哪？

- 參數b ：物件，專門設定該API，比如指定HTTP 請求方法、更改請求封包

指定HTTP 請求方法，預設是GET

  

fetch 是一個主要產生非同步任務的API，主要非同步任務會由promise來實現




#### response.json 

fetch 的promise ：

- resolve則是會回傳代表回應封包的物件

-  若要fetch將回應封包裡的body內的json格式轉換成JS的物件，語法會是

`response.json()`

response.json() 本身也會產生非同步任務來自動轉換，非同步任務是promise


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
- fetch 單純意思為 **去某個地方並從那帶回某個人事物** ，與get不同的是fetch包含 go 和 

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@FetchAPIWeb]]
[[@christineliddleWhatAreUsage]]