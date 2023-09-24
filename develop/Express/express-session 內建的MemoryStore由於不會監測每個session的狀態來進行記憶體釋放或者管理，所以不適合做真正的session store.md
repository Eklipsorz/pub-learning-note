## 描述

若是由express-session套件內建預設的MemoryStore模組來製作和管理session物件，其會在記憶體上分配空間來設置store並從中建立session物件來儲存每一次與客戶端的互動狀態，另外MemoryStore模組本身只是為了測試session而開發，本身不會監測每個session的狀態來進行記憶體釋放或者管理，會有記憶體洩漏問題，所以MemoryStore模組並不適合真正的上線後環境

根據[[@express-sessionExpressjsSessionSimple]]所描述：
> Warning The default server-side session storage, MemoryStore, is purposely not designed for a production environment. It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.

重點：
-  express-session套件內建預設的MemoryStore模組來製作和管理session物件，其會在記憶體上分配空間來設置store並從中建立session物件來儲存每一次與客戶端的互動狀態
-  MemoryStore模組本身只是為了測試session而開發，本身不會監測每個session的狀態來進行記憶體釋放或者管理，會有記憶體洩漏問題，所以MemoryStore模組並不適合真正的上線後環境
- 因此express-session建議開發者使用其他專門實現session store的套件來做




### session store
session store主要有三種形式來實現：
- 以硬碟為主的資料庫來管理session：MongoDB
- 以記憶體為主的資料庫來管理session：Redis
- 以記憶體空間來管理session：Memcached

## 複習
#🧠 express-session 內建的session store-MemoryStore適不適合用在正式開發和部署環境上？ ->->-> `不適合， MemoryStore模組本身只是為了測試session而開發`
<!--SR:!2024-02-29,385,250-->

#🧠 express-session 內建的session store-MemoryStore不適合用在正式開發和部署環境上的原因是什麼？(除了MemoryStore模組本身只是為了測試session而開發以外，提示：記憶體) ->->-> `本身不會監測每個session的狀態來進行記憶體釋放或者管理，會有記憶體洩漏問題`
<!--SR:!2024-06-18,430,230-->


#🧠 session store主要有三種形式來實現 (提示：硬碟、記憶體) ->->-> `以硬碟為主的資料庫來管理session：MongoDB、以記憶體為主的資料庫來管理session：Redis、以記憶體空間來管理session：Memcached`
<!--SR:!2024-01-13,111,208-->

---
Status: #🌱 
Tags:
[[express]] - [[Session]]
Links:
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
References:
[[@jettleeYiCiNodeJs]]
[[@express-sessionExpressjsSessionSimple]]
