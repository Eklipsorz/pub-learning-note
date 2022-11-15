## 描述

[[@mdnSubmitEventWebAPIsa]]
> The SubmitEvent() constructor creates and returns a new SubmitEvent object, which is used to represent a submit event fired at an HTML form.


```
new SubmitEvent(type)
new SubmitEvent(type, options)
```

> ### [Parameters](https://developer.mozilla.org/en-US/docs/Web/API/SubmitEvent/SubmitEvent#parameters "Permalink to Parameters")
> `type`
> A string with the name of the event. It is case-sensitive and browsers always set it to `submit`.

> `options` Optional

> An object that, _in addition of the properties defined in [`Event()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/Event "Event()")_, can have the following properties:

> `submitter` Optional
> An [`HTMLElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) object that is the submit button that triggered the form submission.


```
const form = document.querySelector("form");
const formTrigger = form.querySelector("button.submit");
const submitEvent = new SubmitEvent("submit", { submitter: formTrigger });

form.dispatchEvent(submitEvent);
```

重點：
- SubmitEvent 是一個定義如何產生submit事件信號的介面
- 用途：主要會掛載至特定表單上，藉此定義其表單的submit事件信號如何產生
- 預設下，瀏覽器會替每個表單設定該介面，並定義表單下的提交按鈕被點擊後才產生submit 事件信號給表單
- 語法為：
- 替提交事件名稱取



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[HTML]]
Links:
References:
[[@mdnSubmitEventWebAPIsa]]
