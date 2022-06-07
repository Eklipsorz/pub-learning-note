
## 描述
引用[[@KuaiQuYanSuanFaLRULFU]]所描述：
> -   LRU全稱是Least Recently Used，即最近最久未使用的意思。如果一個數據在最近一段時間沒有被訪問到，那麼在將來它被訪問的可能性也很小。也就是說，當限定的空間已存滿資料時，應當把最久沒有被訪問到的資料淘汰。

> -   LFU（Least Frequently Used）最近最少使用演算法。它是基於“如果一個數據在最近一段時間內使用次數很少，那麼在將來一段時間內被使用的可能性也很小”的思路。  
 > 
 >   注意LFU和LRU演算法的不同之處，LRU的淘汰規則是基於訪問時間，而LFU是基於訪問次數的。
> -   FIFO（First in First out），先進先出。其實在作業系統的設計理念中很多地方都利用到了先進先出的思想，比如作業排程（先來先服務），為什麼這個原則在很多地方都會用到呢？因為這個原則簡單、且符合人們的慣性思維，具備公平性，並且實現起來簡單，直接使用資料結構中的佇列即可實現。在FIFO Cache設計中，核心原則就是：如果一個數據最先進入快取中，則應該最早淘汰掉。

重點：
- 緩存本身容量較小，且肩負著增加存取效率的使命，必須時常釋放空間來存放資訊
- 緩存具體決定哪些資料區塊先被釋放的演算法為：
	- Least Recently Used
	- Least Frequently Used
	- FIFO

### LRU 命名緣由
LRU 全名為Least Recently Used：
- Least 是指在某種程度上少於任何事物，Recently 是指最近地， Used則是指被使用的
- Recently Used 表明為最近有被使用
- 最前面的Least 是形容 Recently Used  來表達在 **最近有使用過的程度上，是很少的**，換言之，離最近使用的時間是最晚的 或者說 在最近一段時間內未被存取
- 強調著離最近使用的時間是最晚的

### LFU 命名緣由
LFU 全名為Least Frequently Used：
- Least 是指在某種程度上少於任何事物，Frequently 是指頻繁地，Used則是指被使用的
- Frequently Used 表明為頻繁地有被使用
- 最前面的Least 是形容 Frequently Used 來表達 在**在頻繁地使用上，是很少的**
- 強調著使用次數


### Least Recently Used 策略

Least Recently Used 的理念為 **最近有使用過的程度上，是很少的**，換言之，離最近使用的時間是最晚的 或者說 在最近一段時間內未被存取，如果一個資料在最近一段時間內都沒存取到，那麼在將來它被存取的可能性也就很小。

基於在概念，當緩存存滿資料，就會先把最近沒有存取到的資料先釋放或者把離最近使用的時間最晚的資料先釋放，通常會選擇後者來方便計算，首先會先取得目前時間或者使用stock來排列這些任務，在這裡先以前者來說明，先計算每個資料最近使用時間相差多少，最大者為離最近使用時間最晚的資料。


拿以下例子來說的話，在這裡有七個資料，每個都標注最近使用時間，現在是12:00 PM，那麼P0對12點來說相差30分鐘，P1則是對12來說相差118分鐘，P2則是相差130分鐘，P3則是223分鐘，P4則是224分鐘，P5則是指306分鐘，P6則是指398分鐘，P7為457分鐘，由於P7是最大的或者離最近使用時間最晚的資料，所以會挑選它為即將要被釋放的資料

[[@LeetCode30Day11146]]
![](https://ithelp.ithome.com.tw/upload/images/20200926/20129147kjPkwvTScH.png)
### Least Frequent Used 策略

[[@LeetCode30Day11146]]:
![](https://ithelp.ithome.com.tw/upload/images/20200926/20129147GAn0gZl15f.png)



## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@KuaiQuYanSuanFaLRULFU]]
[[@LeetCode30Day11146]]