## 描述

deployment steps：

1. test code：確保部署前的應用程式會是沒問題

2. optimize code：添加部署專用的優化代碼並確保沒問題，比如Code Splitting 和 Lazy-loading

3. build app for production：執行特定script來產出一組指定優化代碼，手段會是minify、automatically optimized

4. upload production code to server：將指定優化代碼上傳至主機

5. configure server：設定伺服器主機使它能夠執行指定優化代碼來啟動對應服務

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: