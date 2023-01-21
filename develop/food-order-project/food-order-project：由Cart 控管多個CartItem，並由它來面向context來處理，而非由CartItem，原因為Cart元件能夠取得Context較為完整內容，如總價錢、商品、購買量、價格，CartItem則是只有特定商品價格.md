## 描述


### Cart
由Cart 控管多個CartItem，並由它來面向context來處理，而非由CartItem，原因為Cart元件能夠取得Context較為完整內容，如總價錢、商品、購買量、價格，CartItem則是只有特定商品價格、商品、購買量、價格


在這裡會賦予每個項目的加入至購物車和移除項目的業務邏輯給各個項目上的+ 和 -按鈕：
- + 按鈕會呼叫addItem方法，並指示增加一個對應項目至購物車
-  - 按鈕會呼叫removeItem，並指示移除一個對應項目

```
import { useContext } from 'react';
import React from 'react';
import styles from './Cart.module.css';
import CartItem from './CartItem';
import Modal from '../UI/Modal/Modal';
import CartContext from '../../store/cart-context';

const Cart = (props) => {
  const cartCtx = useContext(CartContext);

  const addToItemHandler = (item) => {
    cartCtx.addItem({
      ...item,
      amount: 1,
    });
  };

  const removeItemHandler = (id) => {
    cartCtx.removeItem(id);
  };

  const totalAmount = cartCtx.totalAmount.toFixed(2);
  const hasItems = cartCtx.items.length > 0;

  return (
    <Modal onClick={props.onHideCart}>
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
      <div className={styles['actions']}>
        <button className={styles['button--alt']} onClick={props.onHideCart}>
          Close
        </button>
        {hasItems && <button>Order</button>}
      </div>
    </Modal>
  );
};

export default Cart;
```



### CartItem

```
import styles from './CartItem.module.css';

const CartItem = (props) => {
  return (
    <div className={styles['cart-item']}>
      <div>
        <h2>{props.name}</h2>
        <div className={styles['summary']}>
          <span className={styles['price']}>{props.price}</span>
          <span className={styles['amount']}>{props.amount}</span>
        </div>
      </div>

      <div className={styles['actions']}>
        <button onClick={props.onRemove}>-</button>
        <button onClick={props.onAdd}>+</button>
      </div>
    </div>
  );
};

export default CartItem;
```


## 複習

#🧠 假使實現購物車的介面和功能是由Cart.js和CartItem.js，Cart.js是呈現每個CartItem的部分以及儲存每個項目的名稱、價格、id，而CartItem則是負責每個項目的渲染和儲存對應項目的id、價格、名稱數量，在這裡為什麼狀態會以Cart.js來去觸發context的更新狀態用函式？而非由CartItem.js->->-> `最主要是要讓CartItem.js是專注呈現每個項目`
<!--SR:!2023-07-20,180,250-->


#🧠 請問為什麼要特意讓每個項目的onAdd和onRemove要以function.protype.bind來重新對應呢？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664553736/blog/react/food-order/function.bind-example_dkgr2n.png) ->->-> `為的就是讓每個項目的onAdd和onRemove都對應著各自項目專屬的增加功能和移除功能，而不透過修改item來實現`
<!--SR:!2023-01-22,72,250-->


#💻 請至/question-review/food-order-project-question領取題目並到install-function-to-cart分支，請試著在Cart.js和CartItem.js中實作替每個item安裝對應+ - 按鈕所要做的事情，請用context來做。 ->->-> `https://github.com/Eklipsorz/food-order-project/tree/main/src/components/Cart`
<!--SR:!2023-01-23,73,250-->


---
Status: #🌱 
Tags:
[[food-order-project]] - [[React]]
Links:
References:



