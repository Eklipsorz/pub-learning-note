
## 描述
鑑於[[Map vs. Filter 差別在於會不會根據原陣列的元素數量來回傳]]



```
const results = products.map(product => {
    if (!productHashTable[product.id]) {
       product.productCategory = productCategory
       productHashTable[product.id] = true
       return product
     }
})
```
  

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
Status: #📥 
Tags:
[[JavaScript]] - [[Array]]
Links:
[[Map vs. Filter 差別在於會不會根據原陣列的元素數量來回傳]]
References:
