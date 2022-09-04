
## 描述
鑑於[[Map vs. Filter 差別在於會不會根據原陣列的元素數量來回傳]]

原本是要設計從product陣列挑出不重複的產品，一開始是使用map方法，結果回傳的新陣列會在原本的重複產品位置上出現undefined-這是因為map會根據原陣列的元素數量來回傳相等數量的陣列，若真的映射不了會直接回傳undefined

```
const results = products.map(product => {
    if (!productHashTable[product.id]) {
       product.productCategory = productCategory
       productHashTable[product.id] = true
       return product
     }
})
```
  
  後來改用filter才真正完成從product陣列挑出不重複的產品且不會出現undefined

```
const results = products.filter(product => {
    if (!productHashTable[product.id]) {
       product.productCategory = productCategory
       productHashTable[product.id] = true
	   return product
    }
})
```



---
Status: #🌱 
Tags:
[[JavaScript]] - [[Array]]
Links:
[[Map vs. Filter 差別在於會不會根據原陣列的元素數量來回傳]]
References:
