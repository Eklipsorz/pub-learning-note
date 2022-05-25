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

### SDS 建立


### 當SDS在被建立後更改字串時的動態調整 
引用[[@redisHIREDIS2022]]所描述的SDS_MAX_PREALLOC會是
```
#define SDS_MAX_PREALLOC (1024*1024)
```


若新存放的字串大小大於目前SDS所分配的buff大小，則會：
- 新存放的字串大小newlen < SDS_MAX_PREALLOC，則新buff的大小會是newlen的兩倍
- 新存放的字串大小 > SDS_MAX_PREALLOC，則新buffer大小就直接為newlen + 1024*1024
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

---
Status: #🌱 
Tags:
[[Redis]] - [[Operating System]]
Links:
References:
[[@redisHIREDIS2022]]
[[@xindooRedisYuanMaPouXiZhiSDSSimpleDynamic]]
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]

