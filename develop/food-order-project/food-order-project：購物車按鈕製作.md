## 描述


### cart-icon 元件

```
const CartIcon = () => {
  return (
    <svg
      xmlns='http://www.w3.org/2000/svg'
      viewBox='0 0 20 20'
      fill='currentColor'
    >
      <path d='M3 1a1 1 0 000 2h1.22l.305 1.222a.997.997 0 00.01.042l1.358 5.43-.893.892C3.74 11.846 4.632 14 6.414 14H15a1 1 0 000-2H6.414l1-1H14a1 1 0 00.894-.553l3-6A1 1 0 0017 3H6.28l-.31-1.243A1 1 0 005 1H3zM16 16.5a1.5 1.5 0 11-3 0 1.5 1.5 0 013 0zM6.5 18a1.5 1.5 0 100-3 1.5 1.5 0 000 3z' />
    </svg>
  );
};

export default CartIcon;

```

### cart-button 元件

```
import styles from './CartButton.module.css';
import CartIcon from './CartIcon';
const CartButton = (props) => {
  return (
    <button className={styles['cart-button']} onClick={props.onClick}>
      <span className={styles['cart-icon']}>
        <CartIcon />
      </span>
      <span>Your Cart</span>
      <span className={styles['cart-badge']}>2</span>
    </button>
  );
};

export default CartButton;
```

### cart-button 樣式
```
.cart-button {
  /* positioning */

  /* display */
  display: flex;
  align-items: center;
  justify-content: space-around;

  /* box model */
  padding: 0.75rem 3rem;
  border-radius: 25px;
  border: none;
  /* font or others */

  font: inherit;
  background-color: #4d1601;
  font-weight: bold;
  color: #fff;
  cursor: pointer;
}

.cart-button:hover,
.cart-button:active {
  /* positioning */
  /* display */
  /* box model */
  /* font or others */
  background-color: #2c0d00;
}

.cart-icon {
  /* positioning */
  /* display */
  /* box model */
  width: 1.35rem;
  height: 1.35rem;
  margin-right: 0.5rem;
  /* font or others */
}

.cart-button:hover .cart-badge,
.cart-button:active .cart-badge {
  /* positioning */
  /* display */
  /* box model */
  /* font or others */
  background-color: #92320c;
}

.cart-badge {
  /* positioning */
  /* display */
  /* box model */
  padding: 0.25rem 1rem;
  border-radius: 25px;
  margin-left: 1rem;
  /* font or others */
  background-color: #b94517;
  font-weight: bold;
}

.bump {
  animation: bump 300ms ease-out;
}

@keyframes bump {
  0% {
    transform: scale(1);
  }
  10% {
    transform: scale(0.9);
  }
  30% {
    transform: scale(1.1);
  }
  50% {
    transform: scale(1.15);
  }
  100% {
    transform: scale(1);
  }
}

```

## 複習


---
Status: #🌱 #📓 
Tags:
[[todo-study]] - [[food-order-project]]
Links:
References: