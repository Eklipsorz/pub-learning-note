## 描述

引述[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]所描述的：
> C语言中也算是支持String了，为什么Redis还要自己封装一个？

> 相较于c原生的字符串，sds多了len、alloc、flag三个字段来存储一些额外的信息，redis考虑到了字符串拼接时带来的巨大损耗，所以每次新建sds的时候会**预分配**一些空间来应对未来的增长，sds和C string的关系熟悉java的旁友可能会决定就好比java中String和StringBuffer的关系。正是因为预留空间的机制，所以redis需要记录下来已分配和总空间大小，当然可用空间可用直接算出来。

重點：
- redis 是以ANSI C語言所撰寫，而C語言本身有字串型別
- redis額外建立新的型別是為了建立能夠動態調整記憶體的字串型別，而這個型別正是Simple Dynamic String。

SDS 字串上的結構與字串結構差別在於前者在一個原本儲存字串的地方中定義四種欄位(如下圖中的len、alloc、flag、buf)，實際上儲存字串的地方是在buf這個欄位，後者則是純放字串，沒len、alloc、flag、buf。
![](https://segmentfault.com/img/bVbRBQC)

SDS在ANSI C實作代碼會是以名為sdshdr (SDS Header)以及實際儲存字串的buf：
- len：紀錄已使用的空間大小
- alloc： 字串實際上能放的空間大小，會是buf大小-1(要計算告知系統為字串的/0 )
- flags：識別用的參數，主要告知系統這是哪些是負責紀錄設定的sdshdr，哪些是實際儲存字串的buf
- buf：實際指向真正能儲存字串的buffer之位置
```
struct __attribute__ ((__packed__)) sdshdr8 {
    uint8_t len; 
    uint8_t alloc; 
    unsigned char flags; 
    char buf[];  
};
struct __attribute__ ((__packed__)) sdshdr16 {
    uint16_t len; 
    uint16_t alloc; 
    unsigned char flags; 
    char buf[];
};
```

### SDS 建立的記憶體
當Redis要分配記憶體空間來儲存字串時，會讓實際儲存字串的記憶體大於實際字串大小，通常會是實際字串大小的一倍，這是為了減緩不必要記憶體調整的次數



### 當SDS在被建立後更改字串時的動態調整 
引用[[@redisHIREDIS2022]]所描述的SDS_MAX_PREALLOC會是
```
#define SDS_MAX_PREALLOC (1024*1024)
```


若新存放的字串大小大於目前SDS所分配的buff大小，則會：
- 新存放的字串大小newlen < SDS_MAX_PREALLOC，則新buff的大小會是newlen的兩倍
- 新存放的字串大小 > SDS_MAX_PREALLOC，則新buffer大小就直接為newlen + 1024*1024，則是為了怕下一次字串會以1024*1024的倍數成長
```
// 扩大sds的实际可用空间，以便后续能拼接更多字符串。 
// 注意：这里实际不会改变sds的长度，只是增加了更多可用的空间(buf)
// avail： buffer目前可用的空間大小，addlen則是(newString-oldString)
// newString 新字串的大小，oldString 舊字串的大小，在這裡一律為前者比後者大

/* 如果有足够的剩余空间，直接返回 */
if (avail >= addlen) return s;

len = sdslen(s);
sh = (char*)s-sdsHdrSize(oldtype);
newlen = (len+addlen);

// 在未超出SDS_MAX_PREALLOC前，扩容都是按2倍的方式扩容，超出后只能递增 
if (newlen < SDS_MAX_PREALLOC)  // SDS_MAX_PREALLOC = 1024*1024
   newlen *= 2;
else
   newlen += SDS_MAX_PREALLOC;
```


但若新存放的字串大小是小於目前SDS所分配的buff大小，那麼就不更改其SDS結構

## 如何在string做處理： 
>   string型別:
 >  1.   取資料：根據redis鍵取對應的整個value值
 >  2.   存資料：根據redis鍵存這個value值
 >  3.   更新資料： 根據redis鍵更新整個value值
 
 重點：
 - 讀取資料：根據key來讀取對應的value
 - 新增資料：根據key來新增對應的value
 - 更新資料：根據key來更新對應的value
 - 移除資料：根據key來移除指定的key-value pair

## 複習
#🧠 Redis Simple Dynamic String 是什麼？ ->->-> `一個能夠根據儲存需求而調整記憶體大小的字串型別，具體來說SDS字串會是由SDShdr和buffer所構成，SDShdr會以4種資料變數分別為len、alloc、flag、buf來分別代表著實際會用到的記憶體大小、目前記憶體還能夠儲存多少個字串、識別字串中哪一個才是SDShdr以及buffer、buffer則是直接定義實際儲存字串的記憶體位置`
<!--SR:!2022-12-19,72,210-->

#🧠 Redis Simple Dynamic String是原生字串嗎？->->-> `並不是，而是為了讓原生字串能夠動態根據需求而調整記憶體的特製字串型別`
<!--SR:!2022-12-22,128,250-->

#🧠 Redis: 當SDS一被建立後，其記憶體大小會是？->->-> `通常一被建立後會是儲存指定的字串，而實際的記憶體會是原字串大小的好幾倍，通常是一倍`
<!--SR:!2023-04-17,198,248-->

#🧠 Redis: 當SDS一被建立後，其記憶體大小為什麼會比要儲存的字串還多？->->-> `這是為了減緩記憶體調整的頻率`
<!--SR:!2023-03-18,180,248-->

#🧠 Redis: 當SDS在被建立後更改字串時的記憶體動態調整會是如何調整？(提示：請以buffer整個空間的大小來思考) ->->-> `若更改的字串大小小於目前buffer還能放的大小，則維持不調整，但若是大於的話，則要考慮其字串大小是否大於1024*1024，若是的話，其buffer大小會是新字串大小+1024*1024，而若不是的話，其buffer大小會是新字串大小的兩倍大`
<!--SR:!2022-12-22,47,228-->


#🧠 Redis Simple Dynamic String 為什麼新字串大小只要大於1024x1024，下一次配置的大小會新字串大小＋1024*1024? ->->-> `則是為了怕下一次字串會以1024*1024的倍數成長`
<!--SR:!2023-03-22,182,248-->

#🧠 Redis string: 如何在string做處理? CRUD ->->-> `讀取資料：根據key來讀取對應的value、新增資料：根據key來新增對應的value、更新資料：根據key來更新對應的value、移除資料：根據key來移除指定的key-value pair`
<!--SR:!2022-12-31,133,250-->

---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]] - [[Operating System]]
Links:
References:
[[@redisHIREDIS2022]]
[[@xindooRedisYuanMaPouXiZhiSDSSimpleDynamic]]
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]

