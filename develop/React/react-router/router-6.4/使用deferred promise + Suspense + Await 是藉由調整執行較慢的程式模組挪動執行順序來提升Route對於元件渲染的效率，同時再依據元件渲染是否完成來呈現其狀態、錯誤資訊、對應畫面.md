## 描述




### 使用deferred promise + Suspense + Await的應用場景

1. Route執行Loader存在執行較慢的程式碼部分，致使元件渲染必須等到其完成才能渲染
2. 適用於不想讓整個頁面的每個頁面都相互等待才渲染，而是能先渲染的元件就先渲染給使用者看，而非等到所有元件都完成渲染才正式渲染給使用者瀏覽
3. 透過Route來實現資料載入、元件渲染載入中的畫面




  
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
- 其用途為將推遲的Promise非同步任務指定特定地點來正式執行其任務，接著等待任務回應回傳就從中取得對應資料來渲染內容和狀況
- Await 語法為：
	- 使用上會使用React 的Suspense來確保還未完成的元件能先有個預設畫面來渲染
	- resolve：形式會是promise。指定以哪個deferred 的promise非同步任務來正式執行和渲染
	- errorElement：形式為JSX Element。當依據deferred 的promise非同步任結果的元件渲染失敗後，就隨之要渲染的錯誤畫面 
	- Children：形式為JSX Element或者會回傳JSX Element 或者 函式物件。當deferred的promise非同步任務是以resolve情況下獲得結果，就直接以Cildren來渲染
		- 若是Children的話，就直接渲染
		- 若是函式物件的話，其引數會是該resolved的結果值，回傳對應JSX Element
```
<Suspense>
	<Await resolve=xxxx1 errorElement=xxxx2>
		<Children>
	</Await>
</Suspense>
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
<!--SR:!2023-04-11,72,250-->

#🧠  suspend 命名緣由會是什麼？ ->->-> `- suspend 是指暫時或者永久停止`
<!--SR:!2023-04-13,73,250-->

#🧠  suspense命名緣由會是什麼？ ->->-> `- suspense 是指呈現被暫時/永久停止的狀態`
<!--SR:!2023-03-11,29,170-->

#🧠 react：Suspense 元件是什麼用途？ ->->-> `用途為以特定內容元件形式來呈現出目前特定元件暫時停止渲染之狀態`
<!--SR:!2023-05-05,84,248-->

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其中為何暫時停止渲染？ ->->-> `由於route還未執行完對應元件的渲染任務，而保持暫時停止渲染`
<!--SR:!2023-02-12,34,248-->

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，具體會是什麼？ ->->-> `則是當Suspense元件包含的元件還未完成render時，就會呈現其對應畫面來表示元件載入中`
<!--SR:!2023-03-30,63,250-->

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其元件語法為何？->->-> `<Suspense fallback={JSX Element}> JSX Element </Suspense>`
<!--SR:!2023-02-22,41,248-->

#🧠 react：Suspense 元件用途為以元件形式來呈現出目前特定元件暫時停止渲染之狀態，其元件語法為`<Suspense fallback={JSX Element}> JSX Element </Suspense>`，其中fallback和JSX Element是做什麼用->->-> `fallback 是當JSX Element 還未完成render時所會替代渲染的內容，而JSX Element則是指著特定元件`
<!--SR:!2023-04-03,65,250-->

#🧠 Suspense 元件源自於哪裡？react-router? react? ->->-> `react`
<!--SR:!2023-03-18,56,250-->

#🧠 React-router：defer 方法是什麼用途？ ->->-> `主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object`
<!--SR:!2023-03-15,53,250-->


#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，其物件會是麼？ ->->-> `該物件夾雜多個屬性，其屬性值為索求特定資源或者資料處理的promise非同步任務`
<!--SR:!2023-02-19,39,248-->


#🧠  React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？ ->->-> `defer(obj)`
<!--SR:!2023-02-25,43,248-->

#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？若要設定特定非同步為deferred task，如何透過defer來用 ->->-> `defer({ attribute1: promise })`
<!--SR:!2023-04-24,72,230-->

#🧠 React-router：defer 方法是主要指定哪些非同步任務為要延遲執行的任務並回傳deferred object，defer語法為？若要設定特定非同步為not-deferred task，如何透過defer來用 ->->-> `defer({ attribute1: await promise })`
<!--SR:!2023-02-14,35,248-->

#🧠 React-router：Await 元件用途是什麼？ ->->-> `其用途為將推遲的Promise非同步任務指定特定地點來正式執行其任務，接著等待任務回應回傳就從中取得對應資料來渲染內容和狀況`
<!--SR:!2023-02-23,39,230-->

#🧠 Await 元件會是屬於誰的？->->-> `Await 元件為React-router所提供的元件`
<!--SR:!2023-03-01,46,248-->


#🧠 React-router：Await 語法為何？ ->->-> `<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>`
<!--SR:!2023-03-24,59,250-->


#🧠 React-router：Await 語法上為何需要Suspense元件？->->-> `確保還未完成的元件能先有個預設畫面來渲染`
<!--SR:!2023-04-01,65,250-->

#🧠 React-router：Await 語法為`<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>` ，其中的resolve會是什麼形式和作用？？ ->->-> ` resolve：形式會是promise。指定以哪個deferred 的promise非同步任務來正式執行和渲染`
<!--SR:!2023-04-12,72,250-->

#🧠 React-router：Await 語法為`<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>` ，其中的errorElement會是什麼形式和作用？？ ->->-> `errorElement：形式為JSX Element。當依據deferred 的promise非同步任結果的元件渲染失敗後，就隨之要渲染的錯誤畫面 `
<!--SR:!2023-04-04,67,250-->


#🧠 React-router：Await 語法為`<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>` ，其中的Children會是什麼形式和作用？？->->-> `形式為JSX Element或者會回傳JSX Element 或者 函式物件。當deferred的promise非同步任務是以resolve情況下獲得結果，就直接以Cildren來渲染`
<!--SR:!2023-03-22,58,250-->


#🧠 React-router：Await 語法為`<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>` ，其中的Children若是JSX Element，會是什麼？ ->->-> `當deferred的promise非同步任務是以resolve情況下獲得結果，就直接以Cildren的JSX Element來渲染`
<!--SR:!2023-03-26,60,250-->


#🧠 React-router：Await 語法為`<Suspense> <Await resolve=xxxx1 errorElement=xxxx2> <Children> </Await> </Suspense>` ，其中的Children若是函式物件，會是什麼？ 會回傳什麼？->->-> `若是函式物件的話，其引數會是該resolved的結果值，回傳對應JSX Element`
<!--SR:!2023-02-17,37,248-->

#🧠 react-router-dom：使用deferred promise + Suspense + Await的應用場景 ->->-> `1. Route執行Loader存在執行較慢的程式碼部分，致使元件渲染必須等到其完成才能渲染 2. 適用於不想讓整個頁面的每個頁面都相互等待才渲染，而是能先渲染的元件就先渲染給使用者看，而非等到所有元件都完成渲染才正式渲染給使用者瀏覽 3. 透過Route來實現資料載入、元件渲染載入中的畫面
<!--SR:!2023-02-28,17,210-->
`




---
Status: #🌱 
Tags:
[[React]]
Links:
[[當loader的部分非同步任務執行過慢，可以透過defer來推遲至component渲染時才開始同時執行，並且根據suspense元件和await元件包覆著推遲任務來根據請求回應和狀態來渲染]]
[[當在async 函式內碰到指定await promise指派給特定識別字時，await會以分配記憶體來定義存放resolve的結果值，並賦予其識別字1，再以promise.then來設定resolve的結果值指派給識別字1所對應的內容]]
References:
[[@ReactTopLevelAPI]]