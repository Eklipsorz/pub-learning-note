## 描述

### boolean expression && JSX element 適用場景

該語法只會在該元件本身就為boolean expression && JSX element 形式才會將被認定為React Element 看待：會先判斷result是否為true，若true才回傳後面的JSX Element；否則不回傳。
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


## 複習

#🧠  boolean expression && JSX element 在怎麼情景下會被當作React Element來處理？ ->->-> `該語法只會在該元件本身就為boolean expression && JSX element 形式才會將被認定為React Element 看待`

#🧠  boolean expression && JSX element 在怎麼情景下會被當作React Element來處理？請用程式碼來表示 ->->-> `return ( result && <ErrorModal onErrorModal={onErrorModalClickHandler}></ErrorModal>);`


#🧠 boolean expression && JSX element 在元件本身就為boolean expression && JSX element 形式下，它是如何運作的？ ->->-> `會先判斷boolean expression是否為true，若true才回傳後面的JSX Element；否則不回傳。`

#🧠  boolean expression && JSX element 若搭配其他元件的話，boolean expression && JSX element 還能正常運作嗎？為什麼？ ->->-> `若混雜其他元件的話，boolean expression && 將被視為一般字串，而非boolean expression，而後者的JSX Element將會直接被當作內容而被渲染`



#🧠 在這裡使用boolean![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743572/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-valid_lyilq3.png)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662743573/blog/frontend/conditional-rendering/boolean-expression-and-jsx-element-invalid_xgb64i.png)->->-> ``

#🧠 請用程式碼來舉例以表示boolean expression && JSX element 若搭配其他元件的話 ->->-> ``


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
References: