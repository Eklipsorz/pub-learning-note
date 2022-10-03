## 描述



### React 適用場景
React memo 適用於
- 不常變更的元件內容
- 規模較大的專案，因為props比對相同緣故而跳過特定branch的virtual dom 結構

#### React.memo(component)的範疇
React.memo(component)
- component A和其component的descendant component會因為同為component A而被記憶體儲存其Virtual DOM並且納入比較來處理，但比較的props會以componet A的內容為主

### React 不適用場景

不適用於
- 時常變更的元件內容，因為不僅沒有用到記憶體內容，還多浪費空間儲存先前props內容和對應virtual dom，以及比較成本
- 以props為基礎來重複使用的元件，如按鈕，本身很有可能會因為props的不同而打造不同內容且同結構的元件
- 規模較小的專案

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React.memo 效能取決於儲存空間成本和計算成本，前者會是props數量、對應元件的Virtual DOM結構、其descendant component的Virtual DOM結構，後者會是props比對成本]]
[[React：React.memo 將特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function]]
References: