## 描述

### Array.map
Array.map 是將指定陣列A的每個元素映射(map)至另一個陣列B的每一個元素，在這裡不論map的callback是否會篩選哪些元素不能映射，皆會以原指定陣列A所擁有的元素數量n來進行映射，也就是另一個陣列B的元素數量還是數量n：
- 若callback 會篩選陣列A中的哪些元素不能映射，不能映射就直接映射成undefined，如下範例：假如陣列儲存20-24，而map只能映射22，那麼結果會是只有22能被映射，其餘則是以undefined
```
let array = [20, 21, 22, 23, 24]

const resultArray = array.map(item => {
	if (item === 22) {
		return item
	}
})
// print [ undefined, undefined, 22, undefined, undefined ]
console.log(resultArray)
```


### Array.filter
Array.filter 則是根據callback 來將原陣列的元素進行篩選，然後將符合篩選條件的元素放置另一個陣列，並於最後回傳
- 將上面的案例改成filter的話，會只剩下22
```
let array = [20, 21, 22, 23, 24]

const resultArray = array.filter(item => {
	if (item === 22) {
		return item
	}
})
// print [22]
console.log(resultArray)	
```
  
### map vs. filter
map 會強調著將原陣列的每個元素都映射一遍，而filter則是強調著從原陣列篩選出符合條件的元素

### 案例
[[Map vs. Filter 差別的實際案例]]

## 複習
#🧠 Array.map 和 Array.filter 的差別 ->->-> `map 會強調著將原陣列的每個元素都映射一遍，而filter則是強調著從原陣列篩選出符合條件的元素`

  
---
Status: #🌱 
Tags:
[[JavaScript]] - [[Array]]
Links:
[[Map vs. Filter 差別的實際案例]]
References:
[[@mdnArrayPrototypeMap]]
[[@mdnArrayPrototypeFilter]]