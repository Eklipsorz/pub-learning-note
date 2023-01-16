## 描述


### 實現按鈕能夠呈現animation效果
目標為：
- 當對應項目按著加入購物車就呈現加入項目的對應動畫

具體實現：

- 定義專門控制animation是否啟用或關閉的狀態-保證動畫能夠一直呈現
	- 具體會以btnIsHightlighted、setBtnIsHighlighted來控制
- 定義能夠根據狀態來產生最後class結果來讓button載入
```
  const cartBtnClasses = `${styles['cart-button']} ${
    btnIsHighlighted ? styles['bump'] : ''
  }`;

  return (
	  <button className={cartBtnClasses} onClick={props.onClick}>
  );
```
- 憑藉第一點來保證動畫會繼續根據加入來呈現動畫，但若貿然放進渲染週期，會引發無限迴圈，因此採取專門處理這問題的useEffect
	- useEffect(callback, \[deps\])
- useEffect 的callback具體定義著：
	- deps設定為items，原因為決定目前互動是否增加的因素為items數量增加以及數量不為0
	- callback：setBtnIsHighlighted(true);來啟用動畫的類別 以及設定300ms timeout任務，其中300ms剛好是動畫持續時間，動畫表演完畢後就透過timeout任務來設定setBtnIsHighlighted(false)將class切換成關閉動畫的類別，另外一點就是錯開batching好方便切換動畫，
	- 定義cleanup 確保不會有多餘的非同步任務要執行以及避免面對大量請求下會呈現出大量動畫的情況

在這裡CSS animation只會執行一次，若要重複執行的話，必須對著指定元件的class持續輪流切換成對應動畫的selector和沒有對應動畫的selector才能不斷呈現出對應動畫


```
import styles from './CartButton.module.css';
import CartIcon from './CartIcon';
import { useContext, useState, useEffect } from 'react';
import CartContext from '../../store/cart-context';

const CartButton = (props) => {
  const cartCtx = useContext(CartContext);
  const [btnIsHighlighted, setBtnIsHighlighted] = useState(false);

  const { items } = cartCtx;
  const numberOfCartItems = items.reduce((curNumber, item) => {
    return curNumber + item.amount;
  }, 0);

  const cartBtnClasses = `${styles['cart-button']} ${
    btnIsHighlighted ? styles['bump'] : ''
  }`;

  useEffect(() => {
    if (!items.length) {
      return;
    }

    setBtnIsHighlighted(true);

    const identifier = setTimeout(() => {
      setBtnIsHighlighted(false);
    }, 300);

    return () => {
      clearTimeout(identifier);
    };
  }, [items]);

  return (
    <button className={cartBtnClasses} onClick={props.onClick}>
      <span className={styles['cart-icon']}>
        <CartIcon />
      </span>
      <span>Your Cart</span>
      <span className={styles['cart-badge']}>{numberOfCartItems}</span>
    </button>
  );
};

export default CartButton;
```

## 複習

#🧠 若元件套用對應selector中的CSS 動畫，那麼動畫會呈現幾次？->->-> `只會呈現一次`
<!--SR:!2023-07-15,180,250-->


#🧠 若元件套用對應selector中的CSS 動畫，那麼動畫會呈現一次，如何重複呈現？->->-> `切換對應元件的class`
<!--SR:!2023-06-16,158,250-->

#💻 請至/question-review/food-order-project-question領取題目並到add-item-animation分支，請試著在CartButton.js中實作出當購物車的項目數量至購物車的動畫，請務必注意每次數量有變動就每次呈現 ->->-> `https://github.com/Eklipsorz/food-order-project/blob/main/src/components/Cart/CartButton.js`
<!--SR:!2023-01-22,73,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References: