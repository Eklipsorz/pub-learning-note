## 描述

### 將CartProvider納入在要對購物車進行處理的介面-清單
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664371397/blog/react/food-order/first-manage-cart_bth3xn.png)

```
import { useRef, useState } from 'react';
import NumberInput from '../UI/Input/NumberInput';
import styles from './MealItemForm.module.css';

const MainItemForm = (props) => {
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

export default MainItemForm;
```

```

```


## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]] - [[React]]
Links:
References: