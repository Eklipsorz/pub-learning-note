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

#🧠 若要確保一旦提交就不會有額外的提交內容，手段可以是什麼？ ->->-> `一旦提交就關閉提交按鈕，按鈕顯示submitting`
<!--SR:!2023-10-06,181,250-->

#🧠 表單一旦提交時，表單元件還能呈現什麼樣子？為什麼？->->-> `顯示不能提交，確保處理部分是以當時提交內容為主`
<!--SR:!2023-08-16,93,230-->

#🧠 useNavigation 是屬於誰的hook?  ->->-> `react-router-dom`
<!--SR:!2024-02-29,240,247-->

#🧠 useNavigation回傳的物件中，state有哪些狀態->->-> `idle、submitting、loading`
<!--SR:!2023-07-14,106,247-->

#🧠 useNavigation回傳的物件中，state有idle、submitting、loading，其中idle狀態會是指什麼？ ->->-> `表示目前沒任何navigation請求要做`
<!--SR:!2023-06-14,90,247-->

#🧠 useNavigation回傳的物件中，state有idle、submitting、loading，其中submitting狀態會是指什麼？ ->->-> `表示目前攔截到提交時的navigation操作並做著對應的action`
<!--SR:!2023-07-19,110,247-->


#🧠 useNavigation回傳的物件中，state有idle、submitting、loading，其中loading狀態會是指什麼？ ->->-> `表示目前攔截到目前router正執行loader來準備資料來給予對應元件做渲染`
<!--SR:!2023-06-26,96,247-->



#🧠 react-router-dom v6.4： useNavigation是什麼用途的hook->->-> `主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料`
<!--SR:!2023-10-17,162,230-->

#🧠 react-router-dom v6.4： useNavigation是主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料的hook，其中資料會有什麼？ ->->-> `導向狀態、導向的目的地、請求內的body部分`
<!--SR:!2023-06-10,50,210-->

#🧠 react-router-dom v6.4： useNavigation是主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料的hook，其hook會回傳什麼？ ->->-> `夾帶著擁有state、location、formData屬性的物件`
<!--SR:!2023-10-02,165,230-->

#🧠 react-router-dom v6.4： useNavigation是主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料的hook，資料包含導向狀態、導向的目的地、請求內的body部分，請問導向狀態有什麼？ ->->-> `1. idle：表示目前沒任何navigation請求要做 2. submitting：表示目前攔截到提交時的navigation操作並做著對應的action 3. loading：表示目前攔截到目前router正執行loader來準備資料來給予對應元件做渲染`
<!--SR:!2023-07-07,15,170-->

#🧠 react-router-dom v6.4： useNavigation是主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料的hook，資料包含導向狀態、導向的目的地、請求內的body部分，請問location會是什麼？->->-> `指定導向的目的地`
<!--SR:!2023-10-08,184,250-->


#🧠 react-router-dom v6.4： useNavigation是主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料的hook，資料包含導向狀態、導向的目的地、請求內的body部分，請問formData會是什麼？->->-> `導向操作所夾帶的body部分`
<!--SR:!2023-10-07,182,250-->


#🧠 react-router-dom 6.4： Navigate vs. useNavigate vs useNavigation 之間差異 ->->-> `1. Navigate 是元件，主要從元件角度實現將使用者導向至指定頁面 2. useNavigate 是hook，主要以程式編碼來將使用者導向至ㄙ指定頁面，會回傳函式物件來進行導向 3. useNavigation 是hook，主要是回傳目前router所攔截到的navigation 操作之目前狀態資料`
<!--SR:!2023-10-21,194,250-->

#🧠  react-router-dom 6.4：useNavigate vs useNavigation 之間差異 ->->-> `1. useNavigate 是hook，主要以程式編碼來將使用者導向至ㄙ指定頁面，會回傳函式物件來進行導向 2. useNavigation 是hook，主要是回傳目前router所攔截到的navigation 操作之目前狀態資料`
<!--SR:!2023-09-16,171,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@UseNavigationV6]]