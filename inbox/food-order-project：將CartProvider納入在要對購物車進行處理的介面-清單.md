## 描述

### 將CartProvider納入在要對購物車進行處理的介面-清單
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664371397/blog/react/food-order/first-manage-cart_bth3xn.png)


MealItem：
- 用途：將擷取到的購買量、名字、id、價格統整起來並呼叫對應context的方法來正式增加項目至購物車
```
import { useContext } from 'react';
import styles from './MealItem.module.css';
import MealItemForm from './MealtemForm';
import CartContext from '../../store/cart-context';

const MealItem = (props) => {
  const cartCtx = useContext(CartContext);
  const addToCartHandler = (amount) => {
    cartCtx.addItem({
      id: props.id,
      name: props.name,
      amount: amount,
      price: props.price,
    });
  };

  return (
    <div className={styles['meal-item']}>
      <div>
        <h3>{props.name}</h3>
        <p className={styles['meal-intro']}>{props.intro}</p>
        <p className={styles['meal-price']}>
          {Number.parseFloat(props.price).toFixed(2)}
        </p>
      </div>
      <MealItemForm id={props.id} onAddToCart={addToCartHandler} />
    </div>
  );
};

export default MealItem;
```


MealItemForm：
- 用途：利用ref物件來對應NumberInput元件下的input DOM節點，以便取得購買量往上傳遞
- 主要會利用提交事件處理函式來擷取對應DOM節點的value，然後呼叫Meal元件所給予的callback往上傳遞資訊
- 細節：
- 在這裡不以context來更新，是因為這個元件並沒有價格和名字這些資訊，頂多只有數量和對應項目的id，所以改使用lifting state up方式來到擁有這些資訊的parent元件，接著再到parent元件上定義一個可以對context做更新的callback
```
import { useRef, useState } from 'react';
import NumberInput from '../UI/Input/NumberInput';
import styles from './MealItemForm.module.css';

const MealItemForm = (props) => {
  const inputRef = useRef();
  const [isValidAmount, setIsValidAmount] = useState(true);
  const cartSubmitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();
    const enteredAmount = inputRef.current.value;
    const enteredAmountNumber = +inputRef.current.value;
    if (
      !enteredAmount.trim().length ||
      enteredAmountNumber < 1 ||
      enteredAmountNumber > 5
    ) {
      setIsValidAmount(false);
      return;
    }

    props.onAddToCart(enteredAmountNumber);
  };

  return (
    <form className={styles.form} onSubmit={cartSubmitHandler} noValidate>
      <NumberInput
        label='Amount'
        attr={{
          id: `meal-item-${props.id}`,
          type: 'number',
          min: '1',
          max: '5',
          step: '1',
          defaultValue: '1',
        }}
        ref={inputRef}
      />
      <button>+ Add</button>
      {!isValidAmount && <p>Please input a amount</p>}
    </form>
  );
};

export default MealItemForm;

```


NumberInput：
- 用途：負責擷取使用者所輸入的購買量
- 主要使用forwardRef 將 MealItemForm的ref 物件轉發至NumberInput下的對應component function來處理，具體則是將ref對應到NumberInput元件下的input DOM節點
```
import { forwardRef } from 'react';
import styles from './NumberInput.module.css';

const NumberInput = forwardRef((props, ref) => {

  return (
    <div className={styles.input}>
      <label htmlFor={props.attr.id}>{props.label}</label>
      <input {...props.attr} ref={ref} />
    </div>
  );
});

export default NumberInput;
```

## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]] - [[React]]
Links:
References: