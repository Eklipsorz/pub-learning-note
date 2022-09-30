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
解法思路為：
- 檢測要新增加的項目是否在購物車內部
- 若有的話，不直接將新增加的項目加入購物車，取而代之，以購物車的項目為主並增加對應數量
- 若沒有的話，就直接將新增加的項目加入購物車

```
import { useReducer } from 'react';
import CartContext from './cart-context';

const initCart = {
  items: [],
  totalAmount: 0,
};

const AddItemToCart = (prevState, payload) => {
  const { items: currentItems } = prevState;

  const updatedTotalAmount =
    prevState.totalAmount + payload.item.price * payload.item.amount;

  const existingItemIndex = currentItems.findIndex(
    (item) => item.id === payload.item.id,
  );

  const existingItem = currentItems[existingItemIndex];
  let updatedItems;
  
  // 若新增項目就已存在在購物車的話
  if (existingItem) {
  
    // 建立一個新的item，除了amount屬性要更新以外，其餘屬性以現有為主
    const updatedItem = {
      ...existingItem,
      amount: existingItem.amount + payload.item.amount,
    };
    
    // 重建一個items
    updatedItems = [...currentItems];
    
    // 在新的items中將已存在購物車的項目以新的item來替代
    updatedItems[existingItemIndex] = updatedItem;
  } else {
	// 若新增項目就不存在購物車的話
    updatedItems = currentItems.concat(payload.item);
  }

  return {
    items: updatedItems,
    totalAmount: updatedTotalAmount,
  };
};

const cartReducer = (prevState, action) => {
  let { type, payload } = action;

  switch (type) {
    case 'ADD_ITEM': {
      const newState = AddItemToCart(prevState, payload);
      return newState;
    }
    case 'REMOVE_ITEM':
      break;
    default:
      return new Error();
  }
};
```

## 複習

#🧠 增加產品至購物車的邏輯會是什麼？ ->->-> `- 檢測要新增加的項目是否在購物車內部 - 若有的話，不直接將新增加的項目加入購物車，取而代之，以購物車的項目為主並增加對應數量 - 若沒有的話，就直接將新增加的項目加入購物車`


#💻 請至/question-review/food-order-project-question領取題目並到add-item-to-cart分支，請試著在CartProvider.js中實作出增加項目至購物車的功能，請務必注意別讓購物車出現重複的項目。 ->->-> `https://github.com/Eklipsorz/food-order-project/blob/main/src/store/CartProvider.js`
<!--SR:!2022-10-04,3,250-->


---
Status: #🌱 
Tags:
[[food-order-project]] - [[React]]
Links:
References: