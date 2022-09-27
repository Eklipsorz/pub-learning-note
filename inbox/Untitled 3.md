## 描述


與版本一相較起來，改善：
1. 藉由少了一層，而提升些許效能
2. 開發/維護難度降低

### 直接透過Modal延伸成存放多個item的Cart



```
import React from 'react';
import styles from './Cart.module.css';
import CartItem from './CartItem';
import Modal from '../UI/Modal/Modal';

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
    <Modal onClick={props.onHideCart}>
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
        <button onClick={props.onHideCart}>Close</button>
        <button>Order</button>
      </div>
    </Modal>
  );
};

export default Cart;

```



### 通用UI - Modal
```
import styles from './Modal.module.css';
import React from 'react';
import ReactDOM from 'react-dom';
const BackDrop = (props) => {
  return <div className={styles.backdrop} onClick={props.onClick}></div>;
};

const ModalOverLay = (props) => {
  return <div className={styles.modal}>{props.children}</div>;
};

const Modal = (props) => {
  return (
    <React.Fragment>
      {ReactDOM.createPortal(
        <BackDrop onClick={props.onClick} />,
        document.getElementById('backdrop-root'),
      )}
      {ReactDOM.createPortal(
        <ModalOverLay>{props.children}</ModalOverLay>,
        document.getElementById('modal-root'),
      )}
    </React.Fragment>
  );
};

export default Modal;
```

## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: