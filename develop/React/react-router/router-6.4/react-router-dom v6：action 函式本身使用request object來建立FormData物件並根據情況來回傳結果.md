## 描述



### request 物件的formData 方法
request object 本身是用fetch api 而建立的。

[[@RequestFormDataWeb]]
> The formData() method of the Request interface reads the request body and returns it as a promise that resolves with a FormData object.

其中request object的 formData方法是  
- 以非同步形式來執行
- 從裡頭接收請求封包中的body部分來轉換成FormData object，具體則是將body部分以key-value pairs形式來封裝成一個物件。


  
### FormData 介面
FormData Object
[[@FormDataWebAPIs]]
> The FormData interface provides a way to easily construct a set of key/value pairs representing form fields and their values, which can then be easily sent using the fetch() or XMLHttpRequest.send() method.
											
重點：
- FormData 介面提供可以將資料包裝成多個key-value pairs形式並以其方式來操作
- 本身提供建構對應物件、屬性、方法：
	- 建構對應物件：其物件本身會是多個key-value pairs形式的資料


### 處理提交表格資料(action)的端點
1. 與表格所在端點一樣的端點，但http動詞會是與獲取表格畫面的http動詞會是不同：
	 - post 為 轉遞表格資料並處理
	 - get 為 獲取表格畫面
2. 與表格所在的端點不一樣的端點


### action 處理表格的基本方式
1. 先從request擷取title和post-text部分
2. 將擷取內容轉換成物件，並以物件來呼叫對應API
3. 根據請求結果來給予錯誤和資訊

```
export async function action({ request }) {
  const formData = await request.formData();

  const post = {
    title: formData.get('title'),
    body: formData.get('post-text'),
  };
  try {
    await savePost(post);
  } catch (error) {
    if (error.status === 422) {
      return error;
    }
    throw error;
  }
  return redirect('/blog');
}
```

其中表單部分要以react-router的Form為主，並調整method和action
```
import { Form } from 'react-router-dom';
import classes from './NewPostForm.module.css';

function NewPostForm({ onCancel, onSubmit, submitting }) {
  return (
    <Form className={classes.form} method='post' action='/blog/new'>
      <fieldset>
        <label htmlFor='title'>Title</label>
        <input id='title' type='text' name='title' required minLength={5} />
      </fieldset>
      <fieldset>
        <label htmlFor='text'>Post Text</label>
        <textarea
          id='text'
          name='post-text'
          required
          minLength={10}
          rows={5}
        ></textarea>
      </fieldset>
      <button type='button' onClick={onCancel} disabled={submitting}>
        Cancel
      </button>
      <button disabled={submitting}>
        {submitting ? 'Submitting...' : 'Create Post'}
      </button>
    </Form>
  );
}

export default NewPostForm;
```

#### action 本身回傳error 和拋出 error 之間不同

  
```
export async function action({ request }) {
  const formData = await request.formData();

  const post = {
    title: formData.get('title'),
    body: formData.get('post-text'),
  };
  try {
    await savePost(post);
  } catch (error) {
    if (error.status === 422) {
      return error;
    }
    throw error;
  }
  return redirect('/blog');
}
```

使用return error 會是將錯誤物件回傳給元件，若是throw error則是被router的錯誤處理給攔截並處理。


### useActionData

[[@UseActionDataV6]]
> This hook provides the returned value from the previous navigation's `action` result, or `undefined` if there was no submission.


重點：
- useActionData 是React-router的hook
- 主要會將React-Router最近一次執行action所獲得的結果回傳至元件使用



## 複習

#🧠 request物件的formData方法會是什麼？ ->->-> `將request包裝的body部分擷取並轉換成以多個key-value pairs形式的資料形式，該形式為formData物件`
<!--SR:!2023-03-26,64,250-->

#🧠 request物件的formData方法會回傳什麼？ ->->-> `回傳FormData物件`
<!--SR:!2023-04-08,73,250-->

#🧠 request物件的formData方法會回傳的FormData物件會是什麼形式？ ->->-> `多個key-value pairs形式的資料形式`
<!--SR:!2023-04-04,70,250-->

#🧠 FormData 介面是什麼？ ->->-> `提供可以將資料包裝成多個key-value pairs形式並以其方式來操作`
<!--SR:!2023-03-22,62,250-->

#🧠 FormData 介面是提供可以將資料包裝成多個key-value pairs形式並以其方式來操作，主要包含了什麼？？ ->->-> `本身提供建構對應物件、屬性、方法`
<!--SR:!2023-03-19,59,250-->

#🧠 處理提交表格資料(action)的端點可以是什麼？ ->->-> `與表格所在端點一樣的端點，但http動詞會是與獲取表格畫面的http動詞會是不同、 與表格所在的端點不一樣的端點`
<!--SR:!2023-03-31,68,250-->

#🧠 處理提交表格資料(action)的端點可以是與表格所在端點一樣的端點，為何可以？->->-> `具體可以設定http動詞為不同來分別做呈現表格和提交`
<!--SR:!2023-04-09,74,250-->

#🧠 處理提交表格資料(action)的端點可以是與表格所在端點一樣的端點，為何可以的原因為設定http動詞為不同來分別做呈現表格和提交，具體會將呈現表格和提交設定什麼？->->-> `端點一樣，	 - post 為 轉遞表格資料並處理 - get 為 獲取表格畫面`
<!--SR:!2023-03-13,55,250-->

#🧠 useActionData 在react-router 中會是什麼hook?  ->->-> `主要會將React-Router最近一次執行action所獲得的結果回傳至元件使用`
<!--SR:!2023-03-27,65,250-->


#🧠 useActionData 在react-router 中會回傳action的執行結果，具體會是什麼時間的結果  ->->-> `主要會將React-Router最近一次執行action所獲得的結果回傳至元件使用`
<!--SR:!2023-02-03,10,250-->


#🧠 react-router-dom v6.4：action 本身回傳error 和拋出 error 之間不同 處在哪？->->-> `使用return error 會是將錯誤物件回傳給元件，若是throw error則是被router的錯誤處理給攔截並處理。`
<!--SR:!2023-04-09,74,250-->

#🧠 react-router-dom v6.4： 以下為action定義，請問以下的回傳error和拋出error之間的不同處在哪？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671114108/blog/react/react-router/v6/action-function/action-function-return-vs-throw_tlgvpy.png) ->->-> ``
<!--SR:!2023-03-17,58,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@UseActionDataV6]]
[[@FormDataWebAPIs]]