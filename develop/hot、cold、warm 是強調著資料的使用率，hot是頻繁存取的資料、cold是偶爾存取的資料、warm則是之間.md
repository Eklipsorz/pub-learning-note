
## 描述

引用[[@ashoksharmaColdVsHot]]所描述的cold、hot意思：
> Generally, the terms “cold” and “hot” mean where the data was located earlier (traditional file storage).
> Accessed frequently, hot data is kept near the CPUs’ heat and the rotating drives. Cold data – data that is not required often – is kept on tape or a drive farther from the data center floor.

牛津字典為
- hot
> new, exciting and very popular


重點：
- hot 在原意上具有新、令人興奮且流行的，cold在原意上則是表達不流行的
- 在電腦科學裡的資料存取會是：
	- hot就是意為頻繁被處理或者存取，而hot data則是頻繁被處理/存取的資料，通常會將頻繁被處理/存取的資料放在離CPU/處理單元較近的地方以方便快速存取
	- cold就是意為偶而被處理或者存取，甚至使用頻率到達未曾再被使用，而cold data偶爾被處理/存取的資料則是放在較遠的地方以讓前者描述的空間能存更多hot data
	- warm 就是意為使用頻率在hot和cold之間，而warm data則是指存取頻率在hot和cold之間的資料
## 複習


#🧠 hot、cold、warm常使用在電腦科學裡的儲存和資料，那麼這些會在那表達成什麼意思？ ->->-> ` hot就是意為頻繁被處理或者存取，而hot data則是頻繁被處理/存取的資料，通常會將頻繁被處理/存取的資料放在離CPU/處理單元較近的地方以方便快速存取、cold就是意為偶而被處理或者存取，甚至使用頻率到達未曾再被使用，而cold data偶爾被處理/存取的資料則是放在較遠的地方以讓前者描述的空間能存更多hot data、warm 就是意為使用頻率在hot和cold之間，而warm data則是指存取頻率在hot和cold之間的資料`
<!--SR:!2022-06-06,3,250-->

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@ashoksharmaColdVsHot]]