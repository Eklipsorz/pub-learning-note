由於採用於stripe 來當金流服務，所以產品價格皆以美金來計算，且為了方便計算，另外結帳時的總金額會以百分比來計算

所以假如是13.94美金的話，那麼數值會是1394


資料庫和緩存上的金額全都以*100的數值結果為主，不會有任何小數點，避免以比整數較為繁雜的浮點數來計算，如：
1000 就是代表著10.00 美金，1023代表著10.23美金

---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References:
