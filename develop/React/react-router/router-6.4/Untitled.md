## 描述


###
20. Building a Multi-Page SPA with React Router

291. Better Data Fetching with React Router 6.4

because you don't have to worry about error handling and loading spinners or anything like that.

because react router manages all these things for you


###


is that you can also defer loading data.

  

react router waits with the page navigation until the data for this page was loaded.

now there are different ways of handling this.

  

e.g.,

1. build some loading bar that's shown until the page is loaded but you might also want to visit the page before the data is there to signal to the user that something's happening

And if that's what you wanna do,

  
### React-router：defer 方法



> this allows you to defer loading data that belong to this page component And you can also defer just parts of the data that's required if you're loading multiple pieces of data.

> This utility allows you to defer values returned from loaders by passing promises instead of resolved values.

重點：
- defer 為React-router-dom的函式
- 主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，該物件夾雜多個屬性，其屬性值為索求特定資源或者資料處理的promise非同步任務
- 語法為：主要會以obj所構成的物件來建構deferred object
	- obj會包含著擁有 **索求特定資源或者資料處理的promise非同步任務** 的屬性值
`defer(obj)`
- 舉例：在這getPosts執行起來會回傳promise
```
defer({ posts: getPosts() })
```

### React-router：Await 元件


> Used to render deferred values with automatic error handling.
> **Note:** `<Await>` expects to be rendered inside of a `<React.Suspense>` or `<React.SuspenseList>` parent to enable the fallback UI.

> resolve
> Takes a promise returned from a deferred loader value to be resolved and rendered.

> children
> Can either be React elements or a function.
> When using a function, the value is provided as the only parameter.

```
<Await resolve={reviewsPromise}>
  {(resolvedReviews) => <Reviews items={resolvedReviews} />}
</Await>

// When using React elements, useAsyncValue will provide the data:

<Await resolve={reviewsPromise}>
  <Reviews />
</Await>;

function Reviews() {
  const resolvedReviews = useAsyncValue();
  return <div>{/* ... */}</div>;
}
```


> Await 的 errorElement：
> to specify which element should be shown if loading that data should fail eventually


重點：
- Await 元件為React-router所提供的元件
- 其用途為將推遲的Promise非同步任務指定特定地點來正式執行，並從中取得對應資料來渲染內容和狀況
- Await 語法為：
	- 使用上會使用React 的Suspense來確保還未完成的元件能先有個預設畫面來渲染
	- resolve：形式會是promise。指定以哪個deferred 的promise非同步任務來正式執行和渲染
	- errorElement：形式為JSX Element。當依據deferred 的promise非同步任結果的元件渲染失敗後，就隨之要渲染的錯誤畫面 
	- Children：形式為JSX Element或者會回傳JSX Element的callback。當deferred的promise非同步任務是以resolve情況下獲得結果，就直接以Cildren來渲染
		- 若是Children的話，就直接渲染
		- 若是callback的話，其引數會是該resolved的結果值，回傳對應JSX Element
```
<Suspense>
	<Await resolve=xxxx1 errorElement=xxxx2>
		<Children>
	</Await>
<Suspense>
```









### Suspense 元件



> that component from code splitting
> react router use this for showing a fallback until that data for which you're waiting is there

[[@ReactTopLevelAPI]]
> `React.Suspense` lets you specify the loading indicator in case some components in the tree below it are not yet ready to render. In the future we plan to let `Suspense` handle more scenarios such as data fetching.


重點：
- Suspense元件 是由React提供
- 用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態
- 具體則是當Suspense元件包含的元件還未完成render時，就會呈現其對應畫面來表示元件載入中
- Suspense 元件語法
	- fallback 為當Sup元件未成功載入就執行渲染其屬性值
`<Suspense fallback={JSX Element}> JSX Element </Suspense>`
```
<Suspense fallback={JSX Element}>
	<Await>
		......
	</Await>
	{......}
</Suspense>
```


### suspense
suspend
> to stop something from being active, either temporarily or permanently

suspense
> the state or condition of being suspended.

重點：
- suspend 是指暫時或者永久停止
- suspense 是指呈現被暫時/永久停止的狀態

### fallback 命名緣由

> A fallback plan or position can be used if other plans do not succeed or other things are not available.

重點：
- fallback 是指計畫失敗時的備案

## 複習

#🧠 fallback 命名緣由會是什麼？ ->->-> `fallback 是指計畫失敗時的備案`

#🧠  suspend 命名緣由會是什麼？ ->->-> `- suspend 是指暫時或者永久停止`

#🧠  suspense命名緣由會是什麼？ ->->-> `- suspense 是指呈現被暫時/永久停止的狀態`

#🧠 react：Suspense 元件是什麼用途？ ->->-> `用途為以特定內容元件形式來呈現出目前特定元件暫時停止渲染之狀態`

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其中為何暫時停止渲染？ ->->-> `由於route還未執行完對應元件的渲染任務，而保持暫時停止渲染`

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，具體會是什麼？ ->->-> `則是當Suspense元件包含的元件還未完成render時，就會呈現其對應畫面來表示元件載入中`

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其元件語法為何？->->-> `<Suspense fallback={JSX Element}> JSX Element </Suspense>`

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其元件語法為`<Suspense fallback={JSX Element}> JSX Element </Suspense>`，其中fallback和JSX Element是做什麼用->->-> `fallback 是當JSX Element 還未完成render時所會替代渲染的內容，而JSX Element則是指著特定元件`

#🧠 Suspense 元件源自於哪裡？react-router? react? ->->-> `react`

#🧠 React-router：defer 方法是什麼用途？ ->->-> `主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object`


#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，其物件會是麼？ ->->-> `該物件夾雜多個屬性，其屬性值為索求特定資源或者資料處理的promise非同步任務`


#🧠  React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？ ->->-> `defer(obj)`

#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？若要設定特定非同步為deferred task，如何透過defer來用 ->->-> `defer({ attribute1: promise })`

#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？若要設定特定非同步為not-deferred task，如何透過defer來用 ->->-> `defer({ attribute1: await promise })`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 
Tags:
[[React]]
Links:
[[當loader的部分非同步任務執行過慢，可以透過defer來推遲至component渲染時才開始同時執行，並且根據suspense元件和await元件包覆著推遲任務來根據請求回應和狀態來渲染]]
[[當在async 函式內碰到指定await promise指派給特定識別字時，await會以分配記憶體來定義存放resolve的結果值，並賦予其識別字1，再以promise.then來設定resolve的結果值指派給識別字1所對應的內容]]
References:
[[@ReactTopLevelAPI]]