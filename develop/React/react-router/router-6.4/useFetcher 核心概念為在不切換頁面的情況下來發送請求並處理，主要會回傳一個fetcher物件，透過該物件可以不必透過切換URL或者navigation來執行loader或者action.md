## 描述

[[@UseFetcherV6]]
> In HTML/HTTP, data mutations and loads are modeled with navigation: \<a href\> and \<form action\>. Both cause a navigation in the browser. The React Router equivalents are \<Link\> and \<Form\>.

> But sometimes you want to call a loader outside of navigation, or call an action (and get the data on the page to revalidate) without changing the URL. Or you need to have multiple mutations in-flight at the same time.

> Many interactions with the server aren't navigation events. This hook lets you plug your UI into your actions and loaders without navigating.

在HTML/HTTP中，資料處理和載入都會由navigation來進行，比如href或者form的action，這些都會導致瀏覽器發生navigation，而在Router則是使用Link和Form元件來發送navigation操作並由Router來攔截。

但有時候你不太想透過navigation或者不太想透過更改URL來呼叫執行loader或者執行action，大部分與伺服器互動都不會是navigation事件，這個hook可以讓你在不用navigation的情況下將你的UI安裝至action和loader

> This is useful when you need to:

> -   fetch data not associated with UI routes (popovers, dynamic forms, etc.)
> -   submit data to actions without navigating (shared components like a newsletter sign ups)
> -   handle multiple concurrent submissions in a list (typical "todo app" list where you can click multiple buttons and all should be pending at the same time)
> -   infinite scroll containers
> -   and more!


> ## `fetcher.submit()`

> The imperative version of `<fetcher.Form>`. If a user interaction should initiate the fetch, you should use `<fetcher.Form>`. But if you, the programmer are initiating the fetch (not in response to a user clicking a button, etc.), then use this function.

> ## [](https://reactrouter.com/en/main/hooks/use-fetcher#fetcherform)`fetcher.Form`

> Just like `<Form>` except it doesn't cause a navigation. (You'll get over the dot in JSX ... we hope!)
```
function SomeComponent() {
  const fetcher = useFetcher();
  return (
    <fetcher.Form method="post" action="/some/route">
      <input type="text" />
    </fetcher.Form>
  );
}
```



重點：
- useFetcher 是 react-router-dom 的hook
- useFetcher 核心概念為在不切換頁面的情況下來發送請求並處理，使服務更像個SPA
- 主要會回傳一個fetcher物件，透過該物件可以不必透過切換URL或者navigation來執行loader或者action
- 負責指定action的主要語法有以下，皆不會透過navigation來切換成對應action所在的URL
	- 若是由使用者互動本身就引發fetch，就使用fetcher.Form
		- method ：形式為字串，為指定轉遞表單資料方法 method
		- action ：形式為路徑字串，為指定處理接收轉遞表單資料
	```
	// syntax
	 <fetcher.Form method=method1 action=action1>
	 </fetcher.Form>
	// example
	  return (
	    <section className={classes.newsletter}>
	      <h2>Sign up for our weekly newsletter</h2>
	      <fetcher.Form method='post' action='/newsletter'>
	        <input
	          ref={emailEl}
	          name='email'
	          id='email'
	          type='email'
	          placeholder='Your email'
	          aria-label='Your email address.'
	        />
	        <button>Sign Up</button>
	      </fetcher.Form>
	    </section>
	  );
	```
	- 若是想由程式碼引發fetch，就使用fetch.submit，具體是模擬表單提交情況
		- body 為物件，主要定義要轉遞的資料
		- options 為物件，主要以method屬性和action屬性來定義method和action
	```
	// syntax
		fetcher.submit(body, options)
	// example 
	    fetcher.submit(
	      // better: use fetcher.Form instead
	      { email: enteredEmail },
	      { method: 'post', action: '/newsletter' }
	    );
	```
-  細節：雖然名義上不以navigation來將頁面導向action、loader所在的path來執行action、loader，但實際上是以path來綁定對應action、loader並用path來呼叫對應action、loader，如同函式呼叫，只是差別在於沒用導向來執行
### 通常設置action專用的useFetcher 方式為
1. 設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader
2. 替action、loader建立一個component來定義
3. 讓想用該action和loader的元件透過useFetcher來建立不透過navigation的表單元件或者透過相關提交方法來處理


#### 設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader

流程會是：
1. 設定能與主要服務/頁面隔離的路徑：具體在Router的路徑陣列中增加一個路徑
2. 替新路徑設定path和action

設定與主要服務/頁面隔離的路徑的原因
	- 確保action、loader所在的path 不會受到Parent Route 給影響

e.g., 
假使action所在的path會是/newsletter，而action會是源自於Newsletter元件所提供的，那麼就引用其內部的action來設定。
```
import { action as newsletterAction } from './pages/Newsletter';

const router = createBrowserRouter([
  // 主要服務/頁面
  {
    path: '/',
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      .....
    ],
  },
  // 隔離的頁面位址
  {
    path: '/newsletter',
    action: newsletterAction,
  },
]);
```

#### 替action、loader建立一個component來定義

```
export async function action({ request }) {
  const data = await request.formData();
  console.log(data.get('email'));

  // send to backend server etc.
}
```


####  讓想用該action和loader的元件透過useFetcher來建立不透過navigation的表單元件或者透過相關提交方法來處理


```
import { useRef } from 'react';
import { useFetcher } from 'react-router-dom';

import classes from './NewsletterSignup.module.css';

function NewsletterSignup() {
  const emailEl = useRef();
  const fetcher = useFetcher();

  // function signupForNewsletterHandler(event) {
  //   event.preventDefault();
  //   const enteredEmail = emailEl.current.value;
  //   // could validate input here
  //   fetcher.submit(
  //     // better: use fetcher.Form instead
  //     { email: enteredEmail },
  //     { method: 'post', action: '/newslestter' },
  //   );
  // }

  return (
    <section className={classes.newsletter}>
      <h2>Sign up for our weekly newsletter</h2>
      <fetcher.Form method='post' action='/newsletter'>
        <input
          ref={emailEl}
          name='email'
          id='email'
          type='email'
          placeholder='Your email'
          aria-label='Your email address.'
        />
        <button>Sign Up</button>
      </fetcher.Form>
    </section>
  );
}

export default NewsletterSignup;
```


### fetcher 命名緣由

重點：
- fetch 本身是移動至特定地方並獲取東西的意思
- fetcher 則是負責實現fetch這動作的一方，在這就是指負責從特定端點對應的action/loader來獲取其回應的程式模組

## 複習

#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-adv領取題目並切換至refactor-with-useFetcher-imp分支，在NewsletterSignup.jsx內使用useFetcher中submit來實現表單提交，記得設定action的path和action ->->-> `https://github.com/academind/react-router-6.4-intro/tree/react-router-6.4-adv/src`
<!--SR:!2023-01-05,11,250-->

#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-adv領取題目並切換至refactor-with-useFetcher-imp分支，在NewsletterSignup.jsx內使用useFetcher中Form元件來實現表單提交，記得設定action的path和action ->->-> ``
<!--SR:!2023-01-05,11,250-->


#🧠 react-router-dom 6.4：useFetcher 是什麼樣的hook？ ->->-> `主要會回傳一個fetcher物件，透過該物件可以不必透過切換URL或者navigation來執行loader或者action`
<!--SR:!2023-01-03,10,250-->

#🧠 react-router-dom 6.4：useFetcher 回傳的fetcher物件是什麼？ ->->-> `透過該物件可以不必透過切換URL或者navigation來執行loader或者action`
<!--SR:!2023-01-03,10,250-->

#🧠 react-router-dom 6.4：useFetcher 回傳的fetcher物件是透過該物件可以不必透過切換URL或者navigation來執行loader或者action，不必透過是什麼意思？或者如何實現 ->->-> `實際上是以path來綁定對應action、loader並用path來呼叫對應action、loader，如同函式呼叫，只是差別在於沒用導向來執行`
<!--SR:!2023-01-22,21,250-->

#🧠 react-router-dom 6.4：useFetcher 核心概念為何？ ->->-> `在不切換頁面的情況下來發送請求並處理，使服務更像個SPA`
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有哪兩個？ ->->-> `fetcher.Form 和 fetcher.submit方法`
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，具體適用於什麼場景->->-> `是由使用者互動本身就引發fetch，就使用fetcher.Form、若是想由程式碼引發fetch，就使用fetch.submit`
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，前者的具體語法會是什麼？->->-> ` <fetcher.Form method=method1 action=action1> ....</fetcher.Form>`
<!--SR:!2023-01-02,9,250-->

#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，前者的具體語法會是`<fetcher.Form method=method1 action=action1> ....</fetcher.Form>`，其中method和action會是什麼形式和作用？ ->->-> `- method ：形式為字串，為指定轉遞表單資料方法 method - action ：形式為路徑字串，為指定處理接收轉遞表單資料`
<!--SR:!2023-01-03,10,250-->

#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，後者的具體語法會是什麼？->->-> `fetcher.submit(body, options)`
<!--SR:!2023-01-20,19,250-->



#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，後者的具體語法會是`fetcher.submit(body, options)`，其中body和options會是什麼形式和用途？ ->->-> `		- body 為物件，主要定義要轉遞的資料 - options 為物件，主要以method屬性和action屬性來定義method和action`
<!--SR:!2023-01-04,10,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，後者的具體語法會是`fetcher.submit(obj1, obj2,.... )`，如何指定method和action？ ->->-> `obj1 至 objN 的其中一個物件得有夾帶action屬性和method屬性的物件`
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，後者的具體語法會是`fetcher.submit(obj1, obj2,.... )`，若沒在obj中設定acction和method，會正常執行嗎？為何 ->->-> `並不會，由於系統就是從obj中決定action和method，若不知道的話，就無法正常執行`
<!--SR:!2023-01-18,18,250-->


#🧠 react-router-dom 6.4：useFetcher 負責指定action的主要語法有fetcher.Form 和 fetcher.submit方法這兩個，後者的具體語法會是`fetcher.submit(obj1, obj2,.... )`，假設要提交email資料以及指定method為post、action為newsletter，請問具體如何設定語法 ->->-> ``
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：通常設置action專用的useFetcher 方式有什麼樣的流程？ ->->-> `1. 設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader 2. 替action、loader建立一個component來定義 3. 讓想用該action和loader的元件透過useFetcher來建立不透過navigation的表單元件或者透過相關提交方法來處理`
<!--SR:!2023-01-15,14,230-->

#🧠 react-router-dom 6.4：通常設置action專用的useFetcher 方式為什麼？設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader，其流程會是什麼？ ->->-> `1. 設定能與主要服務/頁面隔離的路徑：具體在Router的路徑陣列中增加一個路徑 2. 替新路徑設定path和action`
<!--SR:!2023-01-03,10,250-->

#🧠 react-router-dom 6.4：通常設置action專用的useFetcher 方式為什麼？設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader ，隔離原因為何？->->-> `確保action、loader所在的path 不會受到Parent Route 給影響`
<!--SR:!2023-01-03,10,250-->


#🧠 react-router-dom 6.4：通常設置action專用的useFetcher 方式為什麼？設定能與主要服務/頁面隔離的路徑來賦予至action、loader所在的path和對應action、loader ，請用程式碼來表示 ->->-> ``
<!--SR:!2023-01-03,10,250-->

#🧠 fetch 會是什麼意思？ ->->-> `fetch 本身是移動至特定地方並獲取東西的意思`
<!--SR:!2023-01-03,10,250-->

#🧠 fetcher 會是什麼意思？ ->->-> ` fetcher 則是負責實現fetch這動作的一方`
<!--SR:!2023-01-21,20,250-->

#🧠 etch 本身是移動至特定地方並獲取東西的意思，fetcher 則是負責實現fetch這動作的一方，那麼react-router中的useFetcher會是指什麼？請用上述來解釋 ->->-> `在這就是指負責從特定端點對應的action/loader來獲取其回應的程式模組`
<!--SR:!2023-01-02,9,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@UseFetcherV6]]