## 描述

### CartProvider - 增加項目至購物車


#### 結構
1. 使用useReducer 來管理購物車狀態，其中：
	- 使用initCart 定義狀態結構以及初始值
	- 使用cartReducer 定義從dispatch接收到的action來生成對應最新的狀態

2. dispatch 發送的action 結構上會是：
	- 物件形式
	- type屬性定義狀態變更種類
	- payload屬性則是用來輔助reducer來變更狀態


#### 增加項目至購物車 - 初版


```
import { useReducer } from 'react';
import CartContext from './cart-context';

const initCart = {
  items: [],
  totalAmount: 0,
};

const cartReducer = (prevState, action) => {
  let { type, payload } = action;

  switch (type) {
    case 'ADD_ITEM': {
      const updatedItems = prevState.concat(payload.item);
      const updatedTotalAmount =
        prevState.totalAmount + payload.item.price * payload.item.amount;
      return {
        items: updatedItems,
        totalAmount: updatedTotalAmount,
      };
    }
    case 'REMOVE_ITEM':
      break;
    default:
      return new Error();
  }
};

const CartProvider = (props) => {
  const [cartState, cartDispatch] = useReducer(cartReducer, initCart);

  const addItemToCartHandler = (item) => {
    cartDispatch({ type: 'ADD_ITEM', payload: { item } });
  };
  const removeItemFromCartHandler = (id) => {
    cartDispatch({ type: 'REMOVE_ITEM', payload: { id } });
  };

  const cartContext = {
    items: cartState.items,
    totalAmount: cartState.totalAmount,
    addItem: addItemToCartHandler,
    removeItem: removeItemFromCartHandler,
  };

  return (
    <CartContext.Provider value={cartContext}>
      {props.children}
    </CartContext.Provider>
  );
};

export default CartProvider;
```

##### 潛在問題
增加項目至購物車的問題：
- 被增加的項目不會因為是否已先在購物車而先在已存在的購物車項目來更新資料
- 取而代之的是每個新增進來的項目都會直接以新項目的形式來加進購物車項目


#### 針對潛在問題來改良：



## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]] - [[React]]
Links:
References: