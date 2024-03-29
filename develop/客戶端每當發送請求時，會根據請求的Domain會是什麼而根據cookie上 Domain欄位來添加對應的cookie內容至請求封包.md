## 描述


### 客戶端的cookie製作
客戶端的 cookie 是一塊用來記錄與伺服器的過去互動狀態的資料，會根據伺服器的回應是否帶有Set-Cookie才決定是否於客戶端建立cookie，若有的話，就建立；若沒有，就不建立。通常當伺服器想要客戶端儲存目前互動狀態時，伺服器會發送一個擁有Set-Cookie標頭(header)的封包給客戶端，其標頭內容會是以能夠代替這次的互動狀態，其內容形式會是如下(cookie-name和cookie-value即為這次的互動狀態)，客戶端一收到就會根據標頭內容來設置自己的cookie內容為cookie-name:cookie-value，

```
Set-Cookie: <cookie-name>=<cookie-value>; 
```

當客戶端收到之後，就會紀錄伺服器所指定的cookie內容並建立一個cookie，並於每一次向伺服器發送請求封包時，就會在請求封包內附加其cookie內容，形式會是如下

```
Cookie: <cookie-name>=<cookie-value>
```

### cookie內容會紀錄隸屬於哪個伺服器下的哪個位置

每一次客戶端與服器的互動狀態若要紀錄的話，勢必得標記互動狀態是哪個客戶端與哪個伺服器進行互動，在這裡是選擇曾互動的客戶端負責紀錄互動狀態，那麼唯一就差在於**這筆狀態是與哪個伺服器進行互動**，為了方便紀錄，伺服器會要求於Cookie內容以Domain來標記這筆狀態是**與哪個伺服器進行互動**，或者準確地來說，伺服器會設定Domain來**告知客戶端目前Cookie內容是隸屬於哪個伺服器**。

```
Set-Cookie: food=icecream; flavor=cheese; Domain=xxxxx
```

當然同一個伺服器也擁有著不同的路徑，若要更仔細紀錄客戶端到底與哪個路徑進行互動，會使用Path來紀錄。

```
Set-Cookie: food=icecream; flavor=cheese; Domain=xxxxx; Path=xxx
```

總結，具體會是以Domain來指定隸屬於哪個伺服器，而Path則是指定Domain下的哪個路徑：

- Domain：實際標記cookie內容是隸屬於與哪個伺服器下進行互動交流，並且嚴格規範每一次客戶端要附加cookie內容會根據Domain所指定來附加。

- Path：指定Domain下的哪個路徑，並且進一步比對發送請求的Domain和Path來找到對應cookie來附加至請求。

### 客戶端發送請求時

**客戶端每當發送請求時，會根據請求的Domain會是什麼而根據Domain來提供對應的cookie至請求封包**



## 複習

#🧠 客戶端的 cookie 是什麼樣的資料？  ->->-> `是一塊用來記錄與伺服器的過去互動狀態的資料`
<!--SR:!2023-12-10,338,250-->
#🧠 客戶端的cookie 如何產生？ ->->-> `會根據伺服器的回應是否帶有Set-Cookie才決定是否於客戶端建立cookie，若有的話，就建立；若沒有，就不建立`
<!--SR:!2023-11-13,189,230-->
#🧠 伺服器的回應帶有Set-Cookie代表著？ ->->-> `通常當伺服器想要客戶端儲存目前互動狀態時，伺服器會發送一個擁有Set-Cookie標頭(header)的封包給客戶端，其標頭內容會是以能夠代替這次的互動狀態`
<!--SR:!2024-04-29,425,250-->
#🧠 cookie內容會如何紀錄隸屬於哪個伺服器下的哪個位置(提示：以伺服器設定的set-cookie來著手) ->->-> `每一次客戶端與服器的互動狀態若要紀錄的話，勢必得標記互動狀態是哪個客戶端與哪個伺服器進行互動，在這裡是選擇曾互動的客戶端負責紀錄互動狀態，那麼唯一就差在於**這筆狀態是與哪個伺服器進行互動**，為了方便紀錄，伺服器會要求於Cookie內容以Domain來標記這筆狀態是**與哪個伺服器進行互動**，或者準確地來說，伺服器會設定Domain來**告知客戶端目前Cookie內容是隸屬於哪個伺服器**，當然同一個伺服器也擁有著不同的路徑，若要更仔細紀錄客戶端到底與哪個路徑進行互動，會使用Path來紀錄。`
<!--SR:!2024-03-04,204,210-->

#🧠 cookie內容為何被要求紀錄Domain->->-> `是為了方便向過去曾有互動的伺服器發送過去與它之間的處理結果。`
<!--SR:!2024-01-12,358,250-->

#🧠 客戶端發送請求時會何時夾帶cookie? ->->-> `客戶端每當發送請求時，會根據請求的Domain會是什麼而根據Domain來提供對應的cookie至請求封包`
<!--SR:!2024-05-24,439,250-->

---
Status: #🌱 
Tags:
[[Cookie]]
Links:
References: