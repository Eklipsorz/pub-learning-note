
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

## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]]
Links:
References: