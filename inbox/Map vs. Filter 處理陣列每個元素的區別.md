Map vs filter 有趣的區別

1.  Map：若只有在if裡添加return，那麼其餘未滿足if的item皆會設定為undefined，換言之，強迫每一個項目都要有所轉換，不會因為特定條件而丟失

  

map( item => {

if (…) {

return 

}

  

})

1.  filter：不強迫每一個項目都要有所轉換，不會因為特定條件而丟失

  

範例

  
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
Status: #🌱 
Tags:
[[JavaScript]] - [[Array]]
Links:
References: