## 描述





[[@ithomeDay21UseEffect]]
> 所以當你在設計 effect 內的邏輯時，不應該考慮「這個 effect 會在哪幾次 render 時被執行」，而是即使每一次 render 時都執行這個 effect，其邏輯依然能正常運作。因為重點不是哪些 render 會執行這個 effect，或是要經過幾次 render 才能完成這個 effect 想做的事情，而是這個 effect 最後的執行結果能夠「完整的同步」資料的變化就好。

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ithomeDay21UseEffect]]