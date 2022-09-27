
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

## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]]
Links:
References: