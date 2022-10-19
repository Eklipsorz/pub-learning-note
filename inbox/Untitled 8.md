## 描述

custom http hook

回傳：

- isLoading

- error

- sendRequest -> 回傳給其他元件來發送請求

  

製作一個custom hook function

- 業務邏輯保持著通用且能夠讓其他元件使用，盡量不局限於特定項目，方式：
	- 定義設定物件，專門用作於業務邏輯使用
	- 定義額外(並不能成為通用的)函式物件於custom hook function呼叫
- 命名方式保持著通用

## 複習

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：custom hook 在component使用就如同函式呼叫那樣使用，其搭載的hook和custom hook會註冊在該component上]]
[[React：定義 custom hook 以及注意事項]]
References: