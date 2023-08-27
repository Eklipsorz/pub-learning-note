## 描述

### 在渲染層面下，render 函式回傳的內容 是否影響boolean expression && JSX element 正常用途

在渲染層面下，boolean expression && JSX element 只會在render只回傳它本身才會正常作用：會先判斷result是否為true，若true才回傳後面的JSX Element；若false，React會選擇忽略不渲染。
```
return (
	result && <ErrorModal onErrorModal={onErrorModalClickHandler}></ErrorModal>
);
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743572/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-valid_lyilq3.png)

若混雜其他元件的話，boolean expression && 將被視為一般字串，而非boolean expression，而後者的JSX Element將會直接被當作內容而被渲染

```
return (
	<div>
		result && <ErrorModal onErrorModal={onErrorModalClickHandler}></ErrorModal>
	</div>
);
```
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743573/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-invalid_xgb64i.png)


#### render函式若單獨回傳boolean expression && jsx element的話
 render函式若單獨回傳boolean expression && jsx element的話，其boolean expression && jsx element 整個會被React特殊處理：根據boolean expression是否回傳true來決定是否回傳jsx element



 render函式若回傳boolean expression && jsx element的同時夾雜，其boolean expression && jsx element整體會被看作什麼東西？ `boolean expression && 會被當作一般字串，而後頭JSX Element就以JSX元素來看待`

## 複習

#🧠  boolean expression && JSX element 在渲染層面下，什麼樣使用用法下會正常處理前面的語法？ ->->-> `boolean expression && JSX element 只會在render只回傳它、對著JSX元素{expression}替代expression本身才會正常作用`
<!--SR:!2024-10-02,456,250-->

#🧠  boolean expression && JSX element 在渲染層面下，什麼樣使用用法下會正常處理前面的語法？請用程式碼來表示 ->->-> `return ( result && <ErrorModal onErrorModal={onErrorModalClickHandler}></ErrorModal>);`
<!--SR:!2024-06-27,398,250-->


#🧠 boolean expression && JSX element 在元件本身就boolean expression && JSX element 只會在render只回傳它、對著JSX元素{expression}替代expression本身才會正常作用，若正常的話，它是如何運作的？ ->->-> `會先判斷boolean expression是否為true，若true才回傳後面的JSX Element；若false，React會選擇忽略不渲染。`
<!--SR:!2025-01-22,526,250-->

#🧠  boolean expression && JSX element 若搭配其他元件的話，boolean expression && JSX element 還能正常運作嗎？為什麼？ ->->-> `若混雜其他元件的話，boolean expression && 將被視為一般字串，而非boolean expression，而後者的JSX Element將會直接被當作內容而被渲染`
<!--SR:!2025-02-05,538,250-->



#🧠 在渲染層面下，使用boolean expression && JSX element元件分別使用在兩種場景下：沒混雜其他元件和混雜其他元件，請問哪張是沒混雜的版本？哪張是混雜的版本，原因又是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743572/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-valid_lyilq3.png)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743573/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-invalid_xgb64i.png)->->-> ``
<!--SR:!2024-03-18,335,250-->

#🧠 請用程式碼來舉例以表示在渲染層面下，boolean expression && JSX element 若搭配其他元件的話，來變成一般字串和一般React Element->->-> ``
<!--SR:!2023-05-10,151,250-->

#🧠 render函式若單獨回傳boolean expression && jsx element的話，其boolean expression && jsx element整體會被如何處理？？ ->->-> `根據boolean expression是否回傳true來決定是否回傳jsx element`
<!--SR:!2023-12-10,105,230-->


#🧠 render函式若回傳boolean expression && jsx element的同時夾雜其他元件，其boolean expression && jsx element整體會被看作什麼東西？ ->->-> `boolean expression && 會被當作一般字串，而後頭JSX Element就以JSX元素來看待`
<!--SR:!2023-05-22,154,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
[[React：render 函式能夠回傳的JSX Element可以是一般的JSX Element、條件式、陣列形式的JSX Element]]
[[boolean expression && JSX Element案例：混雜其他元件＋boolean expression && JSX Element 未放入到{} vs. 混雜其他元件＋boolean expression && JSX Element 放入到 {}]]
References: