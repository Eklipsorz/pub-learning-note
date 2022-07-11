## 描述

[[@mdnArrayPrototypeSort]] 所描述：
> sort() 方法會原地（in place）對一個陣列的所有元素進行排序，並回傳此陣列

```
arr.sort([compareFunction])
```


> 如果 `compareFunction` 被應用，陣列元素們將根據比較函式之回傳值來排序。如果 `a` 和 `b` 為被比較之兩元素，則：

> -   若 `compareFunction(a, b)` 的回傳值小於 0，則會把 `a` 排在小於 `b` 之索引的位置，即 `a` 排在 `b` 前面。
> -   若 `compareFunction(a, b)` 回傳 0，則 `a` 與 `b` 皆不會改變彼此的順序，但會與其他全部的元素比較來排序。備註：ECMAscript 標準並不保證這個行為，因此不是所有瀏覽器（如 Mozilla 版本在 2003 以前）都遵守此行為。
> -   若 `compareFunction(a, b)` 的回傳值大於 0，則會把 `b` 排在小於 `a` 之索引的位置，即 `b` 排在 `a` 前面。
> 回傳值為
>  排序後的陣列。請注意此為原地（in place）進行排序過的陣列，並且不是原陣列的拷貝。


重點：
- sort 方法不透過額外記憶體來儲存排序子結果的排序方法，具體而言會輪流使用特定比較標準和比較算法來向每一次的比較結果重新排序，直到排序結果已經無法再透過標準和算法來調整結果就停止
- 比較標準會是以compareFunction的回傳值大小是否為比0大、比0小、等於0
- 每一輪都會是以整個陣列的每個元素來比較排序：挑選兩個元素並以比較標準來調整元素在目前陣列上的位置，也就是compareFunction(a,b)來呼叫對應比較標準：
	- 若比較標準回傳比0大：將b元素排在a元素前面 或者說 a元素排在b元素後面
	- 若比較標準回傳比0小：將a元素排在 b元素 前面
	- 若比較標準回傳等於0：不調整a和b兩者的位置


### 案例比較

寫法1

```
const compare = (a, b) => (Date.parse(b.createdAt) - Date.parse(a.createdAt))
products = results.sort(compare)
```

寫法2
```
const compare = (a, b) => (Date.parse(b.createdAt) >= Date.parse(a.createdAt))
products = results.sort(compare)
```


寫法1是正確的，但寫法2會導致錯誤，為什麼？

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnArrayPrototypeSort]]