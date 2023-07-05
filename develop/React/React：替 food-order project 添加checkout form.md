
## 描述

### checkout form 開發目標

> let's make sure that this form only shows up when we click order and that when it shows up
> we actually get rid of these two buttons down there and instead we only showed a confirm button


當按下order 按鈕就顯示checkout form， 接著去除掉order 和 close這兩個按鈕，只留下checkout 表單的Confirm按鈕和Cancel 按鈕


### checkout form 渲染內容部分

form-control：由表單下的各個輸入欄、標籤、錯誤訊息構成
form-actions：由表單下的按鈕構成

```
import styles from './Checkout.module.css';
const Checkout = (props) => {
  return (
    <form>
      <div className={styles['form-control']}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' />
      </div>
      <div className={styles['form-control']}>
        <label htmlFor='street'>Street</label>
        <input type='text' id='street' />
      </div>
      <div className={styles['form-control']}>
        <label htmlFor='postal-code'>Postal Code</label>
        <input type='text' id='postal-code' />
      </div>
      <div className={styles['form-control']}>
        <label htmlFor='city'>City</label>
        <input type='text' id='city' />
      </div>
      <div className={styles['form-actions']}>
        <button type='button' onClick={props.onClose}>
          Cancel
        </button>
        <button>Confirom</button>
      </div>
    </form>
  );
};

export default Checkout;
```


### 將Checkout form 安裝至Cart下

1.  註冊是否顯示checkout 表單的狀態-checkoutIsShown
```
const [checkoutIsShown, setCheckoutIsShown] = useState(false);
```

2. 設定按鈕來設定checkoutIsShown為true
```
const orderHandler = () => {
    setCheckoutIsShown(true);
};
```
3. 添加條件式在渲染部分，來根據checkoutIsShown為true來呈現checkout 表單以及隱藏按鈕部分
```
{checkoutIsShown && <Checkout onClose={props.onHideCart} />}
{!checkoutIsShown && cartAction}
```



#### 完整版
```
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
      {checkoutIsShown && <Checkout onClose={props.onHideCart} />}
      {!checkoutIsShown && cartAction}
    </Modal>
  );
```

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
