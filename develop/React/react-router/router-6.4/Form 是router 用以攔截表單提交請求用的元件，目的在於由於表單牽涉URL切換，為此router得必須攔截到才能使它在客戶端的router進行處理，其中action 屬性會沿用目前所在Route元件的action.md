## 描述


### Form

[[@FormV6]]
> The Form component is a wrapper around a plain HTML form that emulates the browser for client side routing and data mutations. It is not a form validation/state management library like you might be used to in the React ecosystem (for that, we recommend the browser's built in HTML Form Validation and data validation on your backend server).


> ## `action`

> The url to which the form will be submitted, just like [HTML form action](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#attr-action). The only difference is the default action. With HTML forms, it defaults to the full URL. With `<Form>`, it defaults to the relative URL of the closest route in context.

Form：
- react-router-dom所提供的元件
- router 用以攔截表單提交請求用的元件，目的在於由於表單牽涉URL切換，為此router得必須攔截到才能使它在客戶端的router進行處理
- Form 發生提交事件時會產出 request object 來給予router來處理，而非將請求發送至伺服器
- 語法為：
	- method：指定使用哪一種http 動詞來轉遞表格資料
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

#🧠 react-router-dom v6.4：Form 元件會是做什麼？->->-> ` router 用以攔截表單提交請求用的元件`

#🧠 react-router-dom v6.4：Form 元件設計給router來提供的目的是什麼？ ->->-> `目的在於由於表單牽涉URL切換，為此router得必須攔截到才能使它在客戶端的router進行處理`

#🧠 react-router-dom v6.4：若表單套用react-router的Form的話，其提交時的請求會是如何？ ->->-> `該提交時的請求會直接轉向router來處理並呈現對應頁面或者服務`

#🧠  react-router-dom v6.4：若表單沒套用react-router的Form的話，其提交時的請求會是如何？  ->->-> `該提交時的請求會直接轉向伺服器來處理，由伺服器賦予對應頁面或者服務`

#🧠 react-router-dom v6.4：Form 元件語法會是如何？ ->->-> `<Form method=method1 action=action1> </Form>`

#🧠 react-router-dom v6.4：Form 元件語法會是`<Form method=method1 action=action1> </Form>`，其中的method和action分別是什麼？ ->->-> `method：指定使用哪一種http 動詞來轉遞表格資料、action：可填入該請求要發送至哪個端點 或者 指名哪裡是負責處理傳遞資料的地方`

#🧠 react-router-dom v6.4：Form 元件語法會是`<Form method=method1 action=action1> </Form>`，其中的action是可填入該請求要發送至哪個端點 ，請問又可以定義成什麼？ ->->-> `指名哪裡是負責處理傳遞資料的地方`

#🧠 react-router-dom v6.4：router的Form 元件與其他Form套件相比，會是什麼？->->-> `主要差別在於router的Form元件專注在URL切換都轉交由router來處理，不專注資料驗證和狀態管理，後者則是專注在資料驗證和狀態管理`





---
Status: #🌱 
Tags:
[[React]]
Links:
[[Route元件的loader通常要求回傳一個負責資料索求請求的函式物件；Route元件的action通常要求本身能夠回傳回應封包或者回應資料的函式物件]]
References:
[[@FormV6]]
[[@ActionV6]]