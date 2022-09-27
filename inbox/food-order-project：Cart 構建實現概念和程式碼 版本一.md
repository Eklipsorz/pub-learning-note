## 描述



### CartModal 主體內容 - Cart & CartItem

Cart 元件主要會由以下元件構成：
1. 存放多個 CartItem 區域 
2. 計算總價錢的區域
3. 購物車按鈕區塊

#### Cart
```
import React from 'react';
import styles from './Cart.module.css';
import CartItem from './CartItem';


const Cart = (props) => {
  const CartItems = [
    {
      id: 'c1',
      name: 'Sushi',
      price: '22.99',
      amount: 2,
    },
    {
      id: 'c2',
      name: 'Schnitzel',
      intro: 'A german specialty!',
      price: '16.50',
      amount: 5,
    },
  ];

  return (
    <React.Fragment>
      <div className={styles['cart-items']}>
        {CartItems.map((item) => (
          <CartItem
            id={item.id}
            key={item.id}
            name={item.name}
            price={item.price}
            amount={item.amount}
          />
        ))}
      </div>
      <div className={styles['total']}>
        <h3>Total Amount</h3>
        <h3>$33.00</h3>
      </div>
      <div className={styles['actions']}>
        <button>Close</button>
        <button>Order</button>
      </div>
    </React.Fragment>
  );
};

export default Cart;

```

#### CartItem
在這裡的組成：
1. 產品名稱
2. 產品價格 & 產品購買數
3. 產品增加/移除按鈕

```
import styles from './CartItem.module.css';
import Input from '../UI/Input/Input';
const CartItem = (props) => {
  return (
    <div className={styles['cart-item']}>
      <div>
        <h2>{props.name}</h2>
        <div className={styles['summary']}>
          <h3 className={styles['price']}>{props.price}</h3>

          <Input
            attr={{
              id: props.id,
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
        <button>-</button>
        <button>+</button>
      </div>
    </div>
  );
};

export default CartItem;
```

### 從通用UI延伸的Modal - CartModal

在這裡CartModal的主要內容會源自於 Cart 元件。

```
import React from 'react';
import ReactDOM from 'react-dom';
import Cart from './Cart';
import { Modal, BackDrop } from '../UI/Modal/Modal';

const CartModal = (props) => {
  return (
    <React.Fragment>
      {ReactDOM.createPortal(
        <BackDrop onClick={props.onClick} />,
        document.getElementById('backdrop-root'),
      )}
      {ReactDOM.createPortal(
        <Modal onClick={props.onClick}>
          <Cart />
        </Modal>,
        document.getElementById('modal-root'),
      )}
    </React.Fragment>
  );
};

export default CartModal;
```


### 通用UI - Modal & BackDrop
```
import styles from './Modal.module.css';

const BackDrop = (props) => {
  return <div className={styles.backdrop}></div>;
};

const Modal = (props) => {
  return <div className={styles.modal}>{props.children}</div>;
};

export { Modal, BackDrop };
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]] - [[Cart]]
Links:
References: