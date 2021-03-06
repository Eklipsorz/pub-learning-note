


## 軟刪除為主的同步
1. 替每筆在緩存的紀錄增加deleteBit欄位，若刪除就將deleteBit 設定為true；否則就為false：
	- 開發難度：5
	- 缺點：容易出錯/難維護、與資料庫的一致性較差，恐會有永久遺失資訊的可能
	- 優點：存取效能較高
2. 每次刪除購物車項目就將quantity 設為0，然後隔段時間根據quantity=0同步資料庫和緩存
	- 開發難度：2
	- 缺點：與資料庫一致性較差，但可以透過根據現存緩存資料來針對性同步，仍有永久遺失資訊的可能
	- 優點：效能效能較高

## 硬刪除為主的同步
1. 以緩存所擁有的資料為主，隔一段時間就重刷資料庫：
	- 開發難度：3
	- 缺點：刷一次資料庫的成本較高(有一百萬筆就更新一百萬筆)、與資料庫的一致性較差，恐會有永久遺失資訊的可能
	- 優點：簡單、存取效能較高

2. 刪除緩存時就跟著刪除資料庫上的資訊：
	- 開發難度：2
	- 缺點：刪除成本會比單純沒緩存來得慢
	- 優點：與資料庫一致性較高、簡單



## 最後採取方案
軟刪除為主同步的第二方案：
- 與資料庫同步： 設定每日同步資料庫(未來方案)
- 釋放緩存：設定每日同步緩存(未來方案)
- 場景：以面向客戶端最新為主

---
Status: #🌱 
Tags:
[[Caching]] - [[Database]] - [[Side Project]]
Links:
References: