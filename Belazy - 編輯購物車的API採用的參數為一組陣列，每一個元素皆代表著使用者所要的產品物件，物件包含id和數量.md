

Belazy - 編輯購物車的API採用的參數為一組陣列，每一個元素皆代表著使用者所要的產品物件，物件包含id和數量
```
{
	"items": [{"id":"5","quantity":"1"},{"id":"6","quantity":"10"}]
}
```


原本還有另一個版本為以hashMap為底而構成的key-value，key為產品id，value為對應的數量，以上述為例來轉換的話，會是
```
	"5" : "1",
	"6" : "10"
```

---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: