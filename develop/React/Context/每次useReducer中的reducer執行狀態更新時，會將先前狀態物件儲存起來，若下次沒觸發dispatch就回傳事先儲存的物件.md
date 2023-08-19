

## 描述


#### 範例程式碼


```
const [testIsUpdatedReducer, testBegin] = useState(false);

const [emailState, dispatchEmail] = useReducer(emailReducer, {
	value: "",
    isValid: null,
});


const testReducer = () => {
    console.log("test reducer begin");
    testBegin((state) => !state);
};


useEffect(() => {
    console.log("emailState is changed!!!");
}, [emailState]);


return (
	<form>
		..
		..
		..
		<div className={classes.actions}>
          <Button type="submit" className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
          <div className={classes.btn} onClick={testReducer}>
            testReducer
          </div>
        </div>
	</form>
)

```

## 複習
#🧠 React: 請問每次useReducer會是如何執行每個dispatch? 流程是甚麼 ->->-> `先接收dispatch，試著以batch形式來合併各個對應狀態，並最後做一次性的狀態更新和渲染，同時儲存最終的狀態物件`
<!--SR:!2023-08-23,3,250-->

#🧠 React: 請問每次useReducer執行每個dispatch是否會儲存最後處理結果? 若是的話，會是甚麼?  ->->-> `會儲存，儲存最後Batch的狀態結果物件`
<!--SR:!2023-08-23,3,250-->

#🧠  React: 請問每次useReducer執行每個dispatch是會儲存最終的狀態物件，為何儲存? (有兩點)->->-> `效能優化和作為DEPS來使用`
<!--SR:!2023-08-23,3,250-->


#🧠  以下為React的特定元件，請問當點擊testReducer這區塊時，會發生甚麼? 為何? ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692465402/blog/react/useReducer/useReducer-can-store-state-obj-example_tvqc3y.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692465402/blog/react/useReducer/useReducer-can-store-state-obj-example_tvqc3y.png)->->-> `會印出console以及執行render，此時的render會獲得舊有的狀態來渲染`
<!--SR:!2023-08-23,3,250-->


#🧠  以下為React的特定元件，請問當點擊testReducer這區塊時，會因為狀態改變而執行render，請問這一次的render所獲得emailState會是新的嗎? 還是舊有的? 為何? ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692465402/blog/react/useReducer/useReducer-can-store-state-obj-example_tvqc3y.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1692465402/blog/react/useReducer/useReducer-can-store-state-obj-example_tvqc3y.png)->->-> `舊有的，因為useReducer會儲存每一次最後的狀態物件，然而點擊區塊後並未觸發reduer，因而沒要求更改reducer那部分的狀態，所以才繼續以舊有狀態回傳`
<!--SR:!2023-08-23,3,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:


