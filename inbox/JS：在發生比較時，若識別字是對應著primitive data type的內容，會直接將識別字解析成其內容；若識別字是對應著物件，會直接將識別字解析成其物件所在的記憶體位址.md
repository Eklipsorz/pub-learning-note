## 描述

- 在JS中的比較中，若識別字是對應著primitive data type的內容，會以專門儲存primitive value的stack記憶體區塊內容為主
```
let example = 123
// 電腦看到example，就直接看作是123
```
- 在JS中的比較中，若識別字是對應著物件，會以專門儲存reference value的stack記憶體區塊內容為主，也就是以其物件所佔取的heap記憶體區塊位址
```
let example = {}
// 假若{}位置是0x00123，那麼example就會是0x00123
```

## 複習

#🧠 在JS中的比較中，若識別字是對應著primitive data type的內容，會被系統解析成什麼？ ->->-> `會以專門儲存primitive value的stack記憶體區塊內容為主`
<!--SR:!2022-11-10,24,250-->

#🧠 在JS中的比較中，若識別字是對應著物件，識別字會被系統解析成什麼？ ->->-> `會以專門儲存reference value的stack記憶體區塊內容為主，也就是以其物件所佔取的heap記憶體區塊位址`
<!--SR:!2022-12-23,50,250-->


---
Status: #🌱  
Tags:
[[JavaScript]]
Links:
[[primitive data type 是指 電腦環境本身帶有的資料型別，而非程式語言會衍生的，該型別可以在程式語言下，組合成新的資料型別，如物件]]
[[JS：由於物件本身會因為屬性會在執行期間進行任何變動，所以會將物件內容本身儲存在heap記憶體區塊，然後並於stack記憶體區塊儲存對應heap 記憶體位址]]
[[JavaScript 的 primitive data value 和 reference value 本身並不會有執行過程會變更大小的需求，所以會存放於stack記憶體區塊，並用變數名稱作為其區塊的識別名稱]]
References: