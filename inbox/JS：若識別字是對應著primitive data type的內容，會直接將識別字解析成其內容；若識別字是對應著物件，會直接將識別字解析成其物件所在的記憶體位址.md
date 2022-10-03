## 描述

- 在JS中，若識別字是對應著primitive data type的內容，會直接將識別字解析成其內容；
```
let example = 123
// 電腦看到example，就直接看作是123
```
- 在JS中，若識別字是對應著物件，會直接將識別字解析成其物件所在的記憶體位址
```
let example = {}
// 假若{}位置是0x00123，那麼example就會是0x00123
```

## 複習


---
Status: #🌱 #📓 
Tags:
[[JS]]
Links:
[[primitive data type 是指 電腦環境本身帶有的資料型別，而非程式語言會衍生的，該型別可以在程式語言下，組合成新的資料型別，如物件]]
References: