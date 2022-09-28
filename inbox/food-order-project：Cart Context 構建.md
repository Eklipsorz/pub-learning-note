
## 描述



```
import React from 'react';

const CartContext = React.createContext({
  items: [],
  totalAmount: 0,
  addItem: (item) => {},
  removeItem: (id) => {},
});

export default CartContext;
```

items：專門定義購物車目前儲存哪些項目
totalAmount：專門定義購物車目前的總價錢
addItem ：專門增加項目至購物車
removeItem：專門指定哪個項目要從購物車移除


### 增加項目至購物車的邏輯
1. 當增加的項目是存在購物車的話，就直接對對應項目在購物車上的數量進行遞增
2. 當增加的項目是不存在購物車的話，就直接新增項目至購物車並按照購物量來填寫數量

#### 會使用哪個狀態管理？useReducer ? useState
會使用useReducer ，原因在於多個狀態之間會相互影響或者相互改變，比如說判斷要加入的項目是否在購物車作為狀態


### CartProvider
1. 使用useReducer 來管理購物車狀態，其中：
	- 使用initCart 定義狀態結構以及初始值
	- 使用cartReducer 定義從dispatch接收到的action來生成對應最新的狀態

2. dispatch 發送的action 結構上會是：
	- 物件形式
	- type屬性定義狀態變更種類
	- payload屬性則是用來輔助reducer來變更狀態


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


### 將CartProvider納入在要對購物車進行處理的介面-清單

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664371397/blog/react/food-order/first-manage-cart_bth3xn.png)


### 將CartProvider納入在要對購物車進行處理的介面-cart-modal


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664371396/blog/react/food-order/second-manage-cart_qwwbch.png)

## 複習
#🧠 React：以下是用CartContext而製作成的Provider，請問這有什麼潛在問題嗎？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664384045/blog/react/food-order/anti-pattern/cart-context-provider-question_bu7sfz.png) ->->-> `value給定的狀態值一直維持在items為空陣列以及totalAmount為0`

#🧠 React：以下是用CartContext而製作成的Provider，裡面有著狀態值一直被固定的問題，請問如何解決？ ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664384052/blog/react/food-order/anti-pattern/cart-context-provider-question-solution_imc2ok.png)`


---
Status: #🌱 #📓 
Tags:
[[food-order-project]]
Links:
[[food-order-project：將CartProvider納入在要對購物車進行處理的介面-清單]]
References: