## 描述

### 若form的action是由react-router-dom來定義的話

如標頭名稱所示且action會是由client-side router來實現的話，那麼使用HTML原生的form元件去實現action，會直接向目前所在的端點發送post請求，即
```
post http://localhost/blog/new
```

然而該localhost本身並不會提供對應的端點處理，所以會出現404的錯誤訊息。
```
import classes from "./NewPostForm.module.css";

function NewPostForm({ onCancel, onSubmit, submitting }) {
  return (
    <form className={classes.form} method="post" action="/blog/new">
      <fieldset>
        <label htmlFor="title">Title</label>
        <input id="title" type="text" name="title" required minLength={5} />
      </fieldset>
      <fieldset>
        <label htmlFor="text">Post Text</label>
        <textarea
          id="text"
          name="post-text"
          required
          minLength={10}
          rows={5}
        ></textarea>
      </fieldset>
      <button type="button" onClick={onCancel} disabled={submitting}>
        Cancel
      </button>
      <button disabled={submitting}>
        {submitting ? "Submitting..." : "Create Post"}
      </button>
    </form>
  );
}

export default NewPostForm;
```


#### 解法: 改用Form元件替代form
```
import classes from "./NewPostForm.module.css";
import { Form } from "react-router-dom";

function NewPostForm({ onCancel, onSubmit, submitting }) {
  return (
    <Form className={classes.form} method="post" action="/blog/new">
      <fieldset>
        <label htmlFor="title">Title</label>
        <input id="title" type="text" name="title" required minLength={5} />
      </fieldset>
      <fieldset>
        <label htmlFor="text">Post Text</label>
        <textarea
          id="text"
          name="post-text"
          required
          minLength={10}
          rows={5}
        ></textarea>
      </fieldset>
      <button type="button" onClick={onCancel} disabled={submitting}>
        Cancel
      </button>
      <button disabled={submitting}>
        {submitting ? "Submitting..." : "Create Post"}
      </button>
    </Form>
  );
}

export default NewPostForm;

```

## 複習

#💻 請到/githubRepo/react-builder/question-review/react-router-6.4-intro領取題目並切換至refactor-new-post，請在new-post頁面上以router來實現對應提交資料時的action功能，若提交成功就將使用者導向至/blog，若提交內容有誤就在表格上顯示錯誤，若提交失敗就顯示錯誤畫面 ->->-> `https://github.com/academind/react-router-6.4-intro/tree/react-router-6.4-basics`
<!--SR:!2023-04-21,3,250-->


#🧠 若form的action是由react-router-dom來定義且action會是由client-side router來實現的話的話，此時若發生表格提交的話，能夠正常執行嗎? ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681820842/blog/react/form/origin-form-component-in-react_ftgfnj.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681820842/blog/react/form/origin-form-component-in-react_ftgfnj.png)->->-> `那麼使用HTML原生的form元件去實現action，會直接向目前所在的端點發送post請求，即 post http://localhost/blog/new然而該localhost本身並不會提供對應的端點處理，所以會出現404的錯誤訊息。`
<!--SR:!2023-10-15,103,250-->


#🧠 若form的action是由react-router-dom來定義且action會是由client-side router來實現的話的話，此時若發生表格提交的話，能夠正常執行嗎? 若有問題的話，解法概念為何? ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681820842/blog/react/form/origin-form-component-in-react_ftgfnj.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681820842/blog/react/form/origin-form-component-in-react_ftgfnj.png)->->-> `必須將請求導向至client-side router來處理`
<!--SR:!2023-06-23,39,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[使用useNavigation來實現確保一旦提交就不會有額外的提交內容，手段可以是一旦提交就關閉提交按鈕，按鈕顯示submitting]]
[[react-router-dom v6：action 函式本身使用request object來建立FormData物件並根據情況來回傳結果]]
References: