
## 描述
老牌的redis client - node-redis本身有版本上的相容性問題並且導致後續依賴它的套件得跟著出問題，且後面沒金主可以支持開發者，使得整體套件穩定性不高，很容易在開發上出現問題

為了避免版本迭代以及被迫轉換版本較低且功能不多的情況，因而轉換使用ioredis，ioredis 與node-redis 相比的話，具有以下特色：
- 更新/維護頻繁
- 後面有金主可以支持開發者維持第一項


---
Status: #🌱 
Tags:
[[Redis]] - [[Redis Client]]
Links:
[[ioredis - 只要redis client 實例一被建立就會自動連線，若要斷線就必須手動斷線]]
References:
[[@liFeatures2022]]