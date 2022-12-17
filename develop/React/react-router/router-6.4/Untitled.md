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

  

defer =>

this allows you to defer loading data that belong to this page component And you can also defer just parts of the data that's required if you're loading multiple pieces of data.

  

This utility allows you to defer values returned from loaders by passing promises instead of resolved values.

1. defer 回傳deffered object，裡面夾雜了由多個promise構成的屬性值

2. defer 的引數為物件，物件屬性值為對應的promise，舉例

`defer({ posts: funct() })`

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


###

Await 的 errorElement：

to specify which element should be shown if loading that data should fail eventually



### Suspense 元件


> fallback

> that component from code splitting

> react router use this for showing a fallback until that data for which you're waiting is there

> `React.Suspense` lets you specify the loading indicator in case some components in the tree below it are not yet ready to render. In the future we plan to let `Suspense` handle more scenarios such as data fetching.


Suspense元件 => 由React提供

1. 當其元件下面的元件還未完成render時，就會呈現其對應畫面來表示元件載入中
2. 目的為顯示元件未載入時的畫面
3. 元件為如下：
	- fallback 為當以下元件未成功載入就執行渲染其屬性值
`<Suspense fallback={JSX Element} />`

```
<Suspense fallback={JSX Element}>
	<Await>
		......
	</Await>
	{}
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
Status: 
Tags:
Links:
References: