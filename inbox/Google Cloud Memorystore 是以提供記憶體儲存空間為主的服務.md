
Google Cloud Memorystore 是以提供記憶體儲存空間為主的服務
其中有分redis和memcached
- Google Cloud Memorystore for Redis API
- Google Cloud Memorystore for Memcached API


https://github.com/googleapis/nodejs-redis/issues/386





## cloud storage 中的bucket名稱問題
cloud storage 中的bucket名稱會與其他人在自己的cloud storage發生名稱衝突問題：
假如帳號a建立belazy-shop為名稱的專案並於storage建立名為belazy-shop的bucket，而帳號b建立belazy-shop專案並同樣替專案在storage建立名為belazy-shop的bucket，但後者的建立會出現，然而實際上帳號b根本沒在自己的storage擁有的belazy-shop的bucket，為此名稱衝突檢測會是檢測全世界的bucket是否有同樣名稱的belazy-shop
```
Creating gs://belazy-shop/...
ServiceException: 409 A Cloud Storage bucket named 'belazy-shop' already exists. Try another name. Bucket names must be globally unique across all Google Cloud projects, including those outside of your organization.
```

解法只需要在帳號a刪除belazy-shop專案下的名為belazy-shop的水桶，然後再重新在帳號b重建同樣名稱的水桶

gsutil mb gs://belazy-shop                                                   21:26:08
Creating gs://belazy-shop/...


資料庫和客戶端之間可以添加SSL來加強資料傳遞是加密的


---
Status: 
Tags:
Links:
References: