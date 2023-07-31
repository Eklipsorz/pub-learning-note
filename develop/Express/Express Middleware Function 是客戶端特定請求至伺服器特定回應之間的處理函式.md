

## Middleware function

1. Middleware 代表兩個對象之間的程式碼模組，function則是函式，組合在一起就是說明兩個對象之間的程式碼模組是函式

2. Middleware 對於請求X的處理，通常會是由一個針對於請求X的function集合來進行處理，集合中的每一個Middleware function都能處理請求X，並且每個function皆能共享代表request和response的物件，也能對其進行修改，request物件代表著請求X本身，而response物件回應請求X的內容


req & res:
1. req 物件和 res物件是共享於每個請求下的middleware
2. 所有相符特定請求的middleware只允許一個middleware來更改response object


next() ：
- 告知系統可以執行下一個符合當前請求的middleware來執行，本身不會直接呼叫下一個middleware
- 若下一個沒符合的middleware，就停止執行後續的middleware



  