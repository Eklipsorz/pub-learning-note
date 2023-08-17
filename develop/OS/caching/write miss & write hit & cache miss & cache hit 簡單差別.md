
## 描述

> ## More Control in the Application Layer

> In contrast to inline caching, look-aside caching is declarative - the developer tells the application what to cache, not how to do it. For example, with inline caching, the developer must deploy code to the cache server. The developer must also imperatively handle cache misses. The developer optionally deploys code to allow writes to the cache to be pushed into the backing-store either synchronously or asynchronously.

> So, a key difference between inline and look-aside caching patterns is what the application code does versus what the cache does. In the look-aside caching pattern, there is more control in the application layer. In the inline caching pattern, code is deployed into the cache servers, and then the cache takes control of reading from and writing to the backing store.

## 複習


#🧠 write-miss 下有哪些策略可用 ->->-> `allocate no write、allocate on write`

#🧠 write-hit下有哪些策略可用 ->->-> `write through、write behind`

#🧠 cache-miss下有哪些策略可用 ->->-> `read through、read aside`

#🧠 read through 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構? 為什麼 ->->-> `inline caching，因為會需要前者`

#🧠 read aside 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構 ->->-> `look-aside caching`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Caching]] - [[OS]]
Links:
References: