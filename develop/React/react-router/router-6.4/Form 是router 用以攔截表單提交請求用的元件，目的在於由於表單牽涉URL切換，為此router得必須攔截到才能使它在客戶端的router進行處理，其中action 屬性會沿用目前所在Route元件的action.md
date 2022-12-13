## 描述


### Form

[[@FormV6]]
> The Form component is a wrapper around a plain HTML form that emulates the browser for client side routing and data mutations. It is not a form validation/state management library like you might be used to in the React ecosystem (for that, we recommend the browser's built in HTML Form Validation and data validation on your backend server).


> ## `   action`

> The url to which the form will be submitted, just like [HTML form action](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#attr-action). The only difference is the default action. With HTML forms, it defaults to the full URL. With `<Form>`, it defaults to the relative URL of the closest route in context.

Form：
- react-router-dom所提供的元件
- router 用以攔截表單提交請求用的元件，目的在於由於表單牽涉URL切換，為此router得必須攔截到才能使它在客戶端的router進行處理
- Form 發生提交事件時會產出 request object 來給予router來處理，而非將請求發送至伺服器
- 目的為藉由模擬提交表單來讓Router攔截來產生對應URL的頁面或者服務
- 語法為：
	- method：指定使用哪一種http 動詞
	- action：可填入該請求要發送至哪個端點 或者 指名哪裡是負責處理傳遞資料的地方
```
<Form method=method1 action=action1>
	....
</Form>
```
- 細節：
	- 本身並不會做資料驗證、狀態上的管理，只是單純做模擬和攔截




### action 屬性


> React Router version 6.4 also helps with that. And it does help with that by giving you a brand new form component, which you should use if you do want to handle form submission with React Router.

[[@ActionV6]]
> Route actions are the "writes" to route loader "reads".  They provide a way for apps to perform data mutations with simple HTML and HTTP semantics while React Router abstracts away the complexity of asynchronous UI and revalidation. This gives you the simple mental model of HTML + HTTP (where the browser handles the asynchrony and revalidation) with the behavior and UX capabilities of modern SPAs.


> While you can return anything you want from an action and get access to it from useActionData, you can also return a web Response.

重點：
- action 本身是Route元件的屬性
- 目的為模擬表單提交時所會做的提交傳遞和提交資料處理
- 用途為：
	- 主要定義哪一個path是負責處理提交過來的資料進行處理資料處理
- 語法為如下：
	- path為指定哪一個path來處理資料處理
	- callback：會是定義具體的資料處理是為何，其參數為：
		- params 屬性
		- request 屬性
```
<Route path=path1 action={callback} />

const callback = (params, request) => { ... }
```
- action 主要回傳回應封包或者回應結果


## 複習
#🧠

---
Status: #🌱 
Tags:
[[React]]
Links:
[[Route元件的loader通常要求回傳一個負責資料索求請求的函式物件；Route元件的action通常要求本身能夠回傳回應封包或者回應資料的函式物件]]
References:
[[@FormV6]]
[[@ActionV6]]