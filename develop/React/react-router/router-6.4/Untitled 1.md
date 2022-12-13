> React Router version 6.4 also helps with that. And it does help with that by giving you a brand new form component, which you should use if you do want to handle form submission with React Router.

  

Form：

- react-router-dom所提供的元件

- router 用以攔截表單提交請求用的元件，目的在於由於表單牽涉URL切換，為此router得必須攔截到才能使它在客戶端的router進行處理

- Form 發生提交事件時會產出 request object 來給予router來處理，而非將請求發送至伺服器
```
<Form method=method1 action=action1>
	....
</Form>
```

method1：可填入http 動詞
action1：可填入該請求要發送至哪個端點 或者 指名哪裡是負責處理傳遞資料的地方