## 描述




[[@mdnHTMLElementFocusWeb]]
> # HTMLElement.focus()

> The **`HTMLElement.focus()`** method sets focus on the specified element, if it can be focused. The focused element is the element that will receive keyboard and similar events by default.


[[@geeksforgeeksJavaScriptFocus2018]]
> JavaScript focus method is used to give focus to a html element. It sets the element as the active element in the current document. It can be applied to one html element at a single time in a current document. The element can either be a button or a text field or a window etc. It is supported by all the browsers.

重點：
- focus 是指在同一份文件下，將特定元件標記為active element，而被標記的元件會以特定樣式來呈現
- active element 在同一份文件下，只會允許0~1個元件，元件可以是按鈕、文字輸入欄
- focus用法為如下，主要會將HTMLElement對應的元件設定為active element。
```
HTMLElement.focus()
```

## 複習

---
Status: #🌱 #📓 
Tags:
 [[HTML]]
Links:
References:
[[@mdnHTMLElementFocusWeb]]
[[@geeksforgeeksJavaScriptFocus2018]]