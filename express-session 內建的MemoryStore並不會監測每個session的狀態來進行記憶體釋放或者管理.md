若是由express-session套件內建預設的MemoryStore模組來製作和管理session物件，其會在記憶體上分配空間來設置store並從中建立session物件來儲存每一次與客戶端的互動狀態，另外MemoryStore模組本身只是為了測試session而開發，本身不會監測每個session的狀態來進行記憶體釋放或者管理，會有記憶體洩漏問題-**某一些記憶體區塊無法被正常釋放，而這些記憶體區塊還保留值並且不被系統看待成可用的記憶體，造成記憶體上的浪費**，所以MemoryStore模組並不適合真正的上線後環境

> Warning The default server-side session storage, MemoryStore, is purposely not designed for a production environment. It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.

  

不過還是有擅長管理每個session的狀態以及記憶體釋放的第三方套件，比如說：

- 以硬碟為主的資料庫來管理session：MongoDB

- 以記憶體為主的資料庫來管理session：Redis

- 以記憶體空間來管理session：Memcached


---
Status: #📥 
Tags:
Links:
References: