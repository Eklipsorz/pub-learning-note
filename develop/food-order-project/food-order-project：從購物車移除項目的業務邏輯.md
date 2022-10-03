## 描述



從購物車移除一個指定項目：
- 若指定項目的當前數量大於1，就減少對應項目的數量
- 若指定項目的當前數量等於1，就移除整個指定項目

總金額的計算則是以減為主
```
const removeItemFromCart = (prevState, payload) => {
  const { items: currentItems } = prevState;

  const existingItemIndex = currentItems.findIndex(
    (item) => item.id === payload.id,
  );
  const existingItem = currentItems[existingItemIndex];

  let updatedItems;
  if (existingItem.amount === 1) {
    updatedItems = currentItems.filter((item) => item.id !== payload.id);
  } else if (existingItem.amount > 1) {
    const updatedItem = {
      ...existingItem,
      amount: existingItem.amount - 1,
    };
    updatedItems = [...currentItems];
    updatedItems[existingItemIndex] = updatedItem;
  }

  const updatedTotalAmount = prevState.totalAmount - existingItem.price;

  return {
    items: updatedItems,
    totalAmount: updatedTotalAmount,
  };
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
    default:
      return new Error();
  }
};
```


## 複習
#🧠 從購物車移出項目的邏輯會是什麼？ ->->-> `- 若指定項目的當前數量大於1，就減少對應項目的數量 - 若指定項目的當前數量等於1，就移除整個指定項目`
<!--SR:!2022-10-04,3,250-->

#💻 請至/question-review/food-order-project-question領取題目並到remove-item-from-cart分支，請試著在CartProvider.js中實作出從購物車移出指定項目的功能，請務必注意數量為1的項目被移除會發生什麼事情。 ->->-> `https://github.com/Eklipsorz/food-order-project/blob/main/src/store/CartProvider.js`
<!--SR:!2022-10-13,10,250-->




---
Status: #🌱 
Tags:
[[food-order-project]] - [[React]]
Links:
References: