## 描述

先於Cloud SQL的連線設定那邊設定啟用 **Allow only SSL connections** 來強迫每一次客戶端與SQL server都必須是驗證key、ca、cert是否為正確才能允許連線

在這裡我選擇作法為：
- 向Cloud SQL申請key、ca、cert並下載回來
- 將檔案存放至不可被任何人存取的Cloud Storage Bucket
- 設計調用Storage API來讀取Bucket並於Build階段時將key、ca、cert下載至該階段時的專案
(同時開發時期，會根據是否為開發或者線上而不調用SSL來與本地端資料庫連線，但如果是Build時期，就會因為是線上而利用下載回來的key、ca、cert來與Cloud SQL進行連線)


## 任何人下載這個專案時
當任何下載這個專案時，並不會獲取我方的key、ca、cert，只有自己弄出自己的key、ca、cert，才能啟用線上版的功能


---
Status: #📥 
Tags:
[[GCP]] - [[SQL]]
Links:
[[使用Google API必須透過建立對應權限的帳號並從中對應帳號的access-token(key)]]
[[讀取指定google storage bucket下的指定物件]]
References: