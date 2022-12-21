## 描述



### 擁有deps機制的hook擁有特性
1. 利用deps機制來做效能優化
2. 優化手段會是以儲存deps資訊來比較當前deps為主，若一樣就忽略不執行hook，若不一樣就執行hook並儲存目前deps資訊來當作下一次比較
3. 優化手段中若選擇忽略不執行hook通常會是以過去處理過的結果來回傳，節省執行side effect的成本

## 複習

#🧠 React：所有擁有deps機制的hook擁有特性會是什麼？ ->->-> `利用deps機制來做效能優化、優化手段會是以儲存deps資訊來比較當前deps為主、優化手段中若選擇忽略不執行hook通常會是以過去處理過的結果來回傳`
<!--SR:!2023-03-05,74,250-->

#🧠  React：所有擁有deps機制的hook擁有特性會是什麼？以優化手段會是以儲存deps資訊來比較當前deps為主來說是什麼？ ->->-> `若一樣就忽略不執行hook，若不一樣就執行hook並儲存目前deps資訊來當作下一次比較`
<!--SR:!2023-03-05,74,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ithomeDay21UseEffect]]