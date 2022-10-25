

## 描述


### 所需要做的處理

1. 能夠根據表單提交狀態來渲染和對應處理方式，具體可以分為未提交、提交中、已提交。

#### 未提交、提交中、已提交所會有的渲染和處理

根據表單未提交、提交中、已提交來實現對應渲染效果和處理方式
- 未提交：呈現checkout form 和 購物車資料
- 提交中：呈現提交中
- 已提交：呈現已提交完成和關閉按鈕和清除掉購物車資料

### 實現


#### 替cart-context object 增加重置購物車資料功能

/src/store/cart-context.js：替auto-completition註冊clearItems 
```
import React from 'react';

const CartContext = React.createContext({
  items: [],
  totalAmount: 0,
  addItem: (item) => {},
  removeItem: (id) => { },
  clearItems: () => {}
});

export default CartContext;
```

/src/store/CartProvider.js：增加重置的業務邏輯
```
const clearItemsFromCart = () => {
  return { ...initCart };
};

const cartReducer = (prevState, action) => {
  let { type, payload } = action;

  switch (type) {
    case 'ADD_ITEM': {
      const newState = addItemToCart(prevState, payload);
      return newState;
    }
    case 'REMOVE_ITEM': {
      const newState = removeItemFromCart(prevState, payload);
      return newState;
    }
    case 'CLEAR_ITEMS':
    default:
      const newState = clearItemsFromCart();
      return newState;
  }
};
```




## 複習

---
Status: #🌱 
Tags:
Links:
[[React：food-order project 發送請求來獲取meals和建立order]]
[[React：替 food-order project 添加checkout form]]
[[React：替 food-order project 添加custom-hook來發送請求]]
References: