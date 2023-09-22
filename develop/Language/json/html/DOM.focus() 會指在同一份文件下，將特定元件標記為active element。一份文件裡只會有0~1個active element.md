## 描述




[[@mdnHTMLElementFocusWeb]]
> # HTMLElement.focus()

> The **`HTMLElement.focus()`** method sets focus on the specified element, if it can be focused. The focused element is the element that will receive keyboard and similar events by default.


[[@geeksforgeeksJavaScriptFocus2018]]
> JavaScript focus method is used to give focus to a html element. It sets the element as the active element in the current document. It can be applied to one html element at a single time in a current document. The element can either be a button or a text field or a window etc. It is supported by all the browsers.

重點：
- focus 是指在同一份文件下，將特定元件標記為active element，而被標記的元件會以特定樣式、事件處理來呈現。
	- 以特定樣式、事件處理來表現之原因：使該元件與周遭元件之間在呈現上出現差異，好提示使用者所專注的元件是什麼？
- active element 在同一份文件下，只會允許0~1個元件為active element，元件可以是按鈕、文字輸入欄
- focus用法為如下，主要會將HTMLElement對應的元件設定為active element。
```
HTMLElement.focus()
```

## 複習


#🧠 HTML元件的focus是什麼意思？ ->->-> `是指在同一份文件下，將特定元件被標記為active element的行為`
<!--SR:!2024-12-18,506,250-->

#🧠 HTML元件的focus是將特定元件被標記為active element的行為，那麼active element會被瀏覽器設定甚麼來表現？ ->->-> `而被標記的元件會以特定樣式、事件處理來呈現`
<!--SR:!2023-10-05,13,245-->


#🧠 HTML元件被focus標記上active element的話，會有什麼限制？ ->->-> `在同一份文件，只會允許0~1個元件為active element`
<!--SR:!2023-11-06,98,230-->

#🧠 HTML元件中，能被focus標記為active element的元件會是什麼？ ->->-> `按鈕、文字輸入欄`
<!--SR:!2024-05-23,304,210-->

#🧠 在HTML元件中，為何要讓元件被focus後要以特定樣式、特定事件處理來展現其元件？->->-> ` 以特定樣式、事件處理來表現之原因：使該元件與周遭元件之間在呈現上出現差異，好提示使用者所專注的元件是什麼？`
<!--SR:!2023-12-20,253,248-->

#🧠 HTMLElement.focus() 是什麼樣語法？ ->->-> `主要會將HTMLElement對應的元件設定為active element。`
<!--SR:!2024-09-12,436,250-->

#🧠 在DOM API中，哪個語法能將對應元件設定為active element? ->->-> `HTMLElement.focus()`
<!--SR:!2024-04-10,340,250-->



---
Status: #🌱 
Tags:
 [[HTML]]
Links:
References:
[[@mdnHTMLElementFocusWeb]]
[[@geeksforgeeksJavaScriptFocus2018]]