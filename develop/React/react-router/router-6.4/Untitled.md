## 描述


### 確保一旦提交就不會有額外的提交內容
> you also sometimes wanna find out what the current state of the data submission is because whilst we do redirect after data was submitted. we don't do anything whilst the data is being submitted.


確保一旦提交就不會有額外的提交內容，手段可以是：

1. 一旦提交就關閉提交按鈕，按鈕顯示submitting

### useNavigation


[[@UseNavigationV6]]
> This hook tells you everything you need to know about a page navigation to build pending navigation indicators and optimistic UI on data mutations.

> #### `navigation.state`
> -   **idle** - There is no navigation pending. 
> -   **submitting** - A route action is being called due to a form submission using POST, PUT, PATCH, or DELETE 
> -   **loading** - The loaders for the next routes are being called to render the next page


> ## `navigation.location`
> This tells you what the next location is going to be.

> ## `navigation.formData`

> Any POST, PUT, PATCH, or DELETE navigation that started from a \<Form\> or useSubmit will have your form's submission data attached to it. This is primarily useful to build "Optimistic UI" with the submission.formData FormData object.

> In the case of a GET form submission, formData will be empty and the data will be reflected in navigation.location.search.



useNavigation：
-  主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料，包含導向狀態、導向的目的地、請求內的body部分
- 回傳會是物件，其屬性有state、location、formData
- 導向狀態有：navigation.state
	1. idle：表示目前沒任何navigation請求要做
	2. submitting：表示目前攔截到提交時的navigation操作並做著對應的action
	3. loading：表示目前攔截到目前router正執行loader來準備資料來給予對應元件做渲染
- 導向的目的地：navigation.location
- 導向操作所夾帶的body部分：navigation.formData

#### Navigate vs. useNavigate vs useNavigation

1. Navigate 是元件，主要從元件角度實現將使用者導向至指定頁面
2. useNavigate 是hook，主要以程式編碼來將使用者導向至ㄙ指定頁面，會回傳函式物件來進行導向
3. useNavigation 是hook，主要是回傳目前router所攔截到的navigation 操作之目前狀態資料



## 複習



---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@UseNavigationV6]]