

## 前置概念
- Dictionary (HashTable)
[[dictionary 是如同字典一般儲存多個key-value pairs，key會是關鍵字，value則是解釋關鍵字的描述]]


## 設定檔案

- redis.conf
[[redis.conf 是設定Redis 伺服器預設要執行的參數]]

## 型別

- String vs. Hash
[[Redis- String適用場景為讀取場景較多，且更新快取不頻繁；Hash適用場景為更新較為頻繁(尤其是指定特定key)，或者讀取特定key值]]

- Value 主要型別
[[Redis 的Value主要結構為 String 和 Hash]]
[[Redis Hash 遇到 巢狀結構的資料的話，又是面臨到要以String或者Hash來儲存的問題]]

- Simple Dynamic String
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]

- Hash
[[Redis Hash是儲存多個key-value的字典]]

## 模組

- RedisJSON
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]

- 問題：若一開始於Redis載入RedisJSON模組並設定JSON格式的value讓其儲存db的話，接著若以沒載入其模組的情況下執行Redis Server 會出錯
[[Redis 伺服器若讀取到錯誤格式的資料庫會無法執行]]


- RedisJSON JSONPath
[[RedisJSON JSONPath 是RedisJSON開發人員所針對JSONPath概念而開發出來的產品]]