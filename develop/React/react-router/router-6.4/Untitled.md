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


### 處理表格資料(action)的端點
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

if i return here instead of throwing error, i stay on this page.

I don't redirect away and i don't load the error page

  

使用return error 會是將錯誤物件回傳給元件，若是throw error則是被router錯誤處理給攔截並顯示錯誤畫面。

  

會使用useActionData來替代，

主要用途為從最近一次執行的action function獲取其回傳結果

> This hook provides the returned value from the previous navigation's `action` result, or `undefined` if there was no submission.



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@FormDataWebAPIs]]