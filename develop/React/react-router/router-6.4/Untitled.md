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
- 主要回傳deferred object，該物件夾雜多個屬性，其屬性值為索求特定資源或者資料處理的promise非同步任務
- 語法為：主要會以obj所構成的物件來建構deferred object
	- obj會包含著擁有 **索求特定資源或者資料處理的promise非同步任務** 的屬性值
`defer(obj)`
- 舉例：在這getPosts執行起來會回傳promise
```
defer({ posts: getPosts() })
```

###

Await =>

1. Component

2. 主要用來渲染被延遲的內容並根據載入

> Used to render deferred values with automatic error handling.

3.

<Await resolve={}> </Await>

  

resolve：

主要填入回傳deferred loader value的promise

> Takes a promise returned from a deferred loader value to be resolved and rendered.

  

  

`children`

回傳對應

>  Can either be React elements or a function.

> When using a function, the value is provided as the only parameter.




Await 的 errorElement：

to specify which element should be shown if loading that data should fail eventually



### Suspense 元件



> that component from code splitting
> react router use this for showing a fallback until that data for which you're waiting is there

[[@ReactTopLevelAPI]]
> `React.Suspense` lets you specify the loading indicator in case some components in the tree below it are not yet ready to render. In the future we plan to let `Suspense` handle more scenarios such as data fetching.


重點：
- Suspense元件 是由React提供
- 用途為以元件形式來呈現出目前暫時停止特定元件的渲染之狀態
- 具體則是當Suspense元件包含的元件還未完成render時，就會呈現其對應畫面來表示元件載入中
- Suspense 元件語法
	- fallback 為當以下元件未成功載入就執行渲染其屬性值
`<Suspense fallback={JSX Element} />`
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
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
[[當loader的部分非同步任務執行過慢，可以透過defer來推遲至component渲染時才開始同時執行，並且根據suspense元件和await元件包覆著推遲任務來根據請求回應和狀態來渲染]]
References:
[[@ReactTopLevelAPI]]