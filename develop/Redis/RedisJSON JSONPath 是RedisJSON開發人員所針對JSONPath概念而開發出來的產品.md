## 描述

引用[[@redisPath]]所描述：

> Since no standard for path syntax exists, RedisJSON implements its own. RedisJSON's syntax is based on common best practices and intentionally resembles [JSONPath](http://goessner.net/articles/JsonPath/).

重點：
- JSONPath 語言本身沒有官方組織上的標準，所以市面上會有許多實現其語言概念的實作，如RedisJSON JSONPath


## 複習

#🧠 JSONPath 有官方組織上的標準嗎？->->-> `並沒有，只有概念`
<!--SR:!2023-03-29,187,250-->

#🧠 RedisJSON JSONPath是什麼 ->->-> `是RedisJSON的開發人員針對JSONPath概念而實現的產品，屬於Redis官方本身的JSONPath 實現`
<!--SR:!2023-03-01,39,230-->

---
Status: #🌱 
Tags:
[[JSON]] - [[connect-redis 支援 redis 4.x (npm) 必須要添加 legacyMode 為true的參數]]
Links:
[[JSONPath 是基於JSON樹狀結構而提供一系列語法來找尋對應樹狀節點的語言]]
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]
References:
[[@redisPath]]