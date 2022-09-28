## 描述


### Cart
由Cart 控管多個CartItem，並由它來面向context來處理，而非由CartItem，原因為Cart元件能夠取得Context較為完整內容，如總價錢、商品、購買量、價格，CartItem則是只有特定商品價格、商品、購買量、價格

```
import { useContext } from 'react';
import React from 'react';
import styles from './Cart.module.css';
import CartItem from './CartItem';
import Modal from '../UI/Modal/Modal';
import CartContext from '../../store/cart-context';

const Cart = (props) => {
  const cartCtx = useContext(CartContext);
  const addToItemHandler = () => {};
  const removeItemHandler = () => {};
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
            onAdd={addToItemHandler.bind(null, item.id)}
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
import NumberInput from '../UI/Input/NumberInput';
const CartItem = (props) => {
  return (
    <div className={styles['cart-item']}>
      <div>
        <h2>{props.name}</h2>
        <div className={styles['summary']}>
          <h3 className={styles['price']}>{props.price}</h3>

          <NumberInput
            attr={{
              id: `cart-item-${props.id}`,
              type: 'number',
              min: '1',
              max: '99',
              step: '1',
              defaultValue: props.amount,
            }}
          />
        </div>
      </div>

      <div className={styles['actions']}>
        <button onRemove={props.onRemove}>-</button>
        <button onAdd={props.onAdd}>+</button>
      </div>
    </div>
  );
};

export default CartItem;
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]] - [[React]]
Links:
References:



