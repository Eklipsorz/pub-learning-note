

## 描述


### 所需要做的處理

1. 能夠根據表單提交狀態來渲染和對應處理方式，具體可以分為未提交、提交中、已提交。

#### 未提交、提交中、已提交所會有的渲染和處理

根據表單未提交、提交中、已提交來實現對應渲染效果和處理方式
- 未提交：呈現checkout form 和 購物車資料
- 提交中：呈現提交中
- 已提交：呈現已提交完成和關閉按鈕和清除掉購物車資料

### 實現

未提交會有的內容：
```
  const cartContent = (
    <React.Fragment>
      <div className={styles['cart-items']}>
        {cartCtx.items.map((item) => (
          <CartItem
            id={item.id}
            key={item.id}
            name={item.name}
            price={item.price}
            amount={item.amount}
            onAdd={addToItemHandler.bind(null, item)}
            onRemove={removeItemHandler.bind(null, item.id)}
          />
        ))}
      </div>

      <div className={styles['total']}>
        <h3>Total Amount</h3>
        <h3>${totalAmount}</h3>
      </div>
      {checkoutIsShown && (
        <Checkout onClose={props.onHideCart} onConfirom={confirmHandler} />
      )}
      {!checkoutIsShown && cartAction}
    </React.Fragment>
  );
```

提交中會有的內容
```
const submittingContent = <p>Submitting data to server...</p>;
```

提交完成時會有的內容：
```
const didSubmitContent = (
    <React.Fragment>
      <p>Successfully Submit Data to Server</p>
      <div className={styles['actions']}>
        <button className={styles['button--alt']} onClick={props.onHideCart}>
          Close
        </button>
      </div>
    </React.Fragment>
  );
```

Cart元件整體渲染部分：
```
  return (
    <Modal onClick={props.onHideCart}>
      {isSubmitting && submittingContent}
      {isSubmitted && didSubmitContent}
      {!isSubmitted && !isSubmitting && cartContent}
    </Modal>
  );
```

### 根據表單未提交、提交中、已提交來實現對應渲染效果和處理方式

- 註冊提交中、已提交這兩種狀態
```
const [isSubmitting, setIsSubmitting] = useState(false);
const [isSubmitted, setIsSubmitted] = useState(false);
```
- 更新提交狀態、呼叫清除掉購物車資料之方法
```
  const confirmHandler = async (userData) => {
    const options = {
      url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/orders.json',
      method: 'POST',
      headers: { 'content-type': 'application/json' },
      body: JSON.stringify({
        user: userData,
        orderedItems: cartCtx.items,
      }),
    };

    setIsSubmitting(true);
    setIsSubmitted(false);
    const response = await createCartData(options);
    setIsSubmitting(false);
    setIsSubmitted(true);

    cartCtx.clearItems();
  };
```


#### 替cart-context object 增加重置購物車資料功能

/src/store/cart-context.js：替auto-completition註冊clearItems 
```
import React from 'react';

const CartContext = React.createContext({
  items: [],
  totalAmount: 0,
  addItem: (item) => {},
  removeItem: (id) => { },
  clearItems: () => {}
});

export default CartContext;
```

/src/store/CartProvider.js：增加重置的業務邏輯
```
const clearItemsFromCart = () => {
  return { ...initCart };
};

const cartReducer = (prevState, action) => {
  let { type, payload } = action;

  switch (type) {
    case 'ADD_ITEM': {
      const newState = addItemToCart(prevState, payload);
      return newState;
    }
    case 'REMOVE_ITEM': {
      const newState = removeItemFromCart(prevState, payload);
      return newState;
    }
    case 'CLEAR_ITEMS':
    default:
      const newState = clearItemsFromCart();
      return newState;
  }
};
```

替cart-provider 註冊clearItems 這方法
```
 const clearItemsFromCartHandler = () => {
    cartDispatch({ type: 'CLEAR_ITEMS' });
  };

  const cartContext = {
    items: cartState.items,
    totalAmount: cartState.totalAmount,
    addItem: addItemToCartHandler,
    removeItem: removeItemFromCartHandler,
    clearItems: clearItemsFromCartHandler
  }
```

## 複習

#💻 請至/react-builder/question-review/food-order-project-question領取題目並切換至develop-checkout-form 分支，實現一個checkout form 會有的功能-付款功能、付款資料表單和按鈕之間的切換、付款成功的視窗、付款載入狀況、付款錯誤顯示->->-> `https://github.com/academind/react-complete-guide-code/tree/17-practice-food-order-http-forms/code/07-finished/src`
<!--SR:!2022-12-10,3,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：food-order project 發送請求來獲取meals和建立order]]
[[React：替 food-order project 添加checkout form]]
[[React：替 food-order project 添加custom-hook來發送請求]]
References: