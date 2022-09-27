## 描述

首先先製作假資料來表示購物車資料



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
[[food-order-project]]
Links:
References: