## 描述

引用[[@xiadayuErJinZhiAnQuanBinarySafe]]所描述：

> redis中SDS的实现保证了redis保存的数据是二进制安全的.
```text
struct sdshdr {
    int len;
    int free;
    char buf[];
};
```
> 它并不像C语言那样,使用'\0'作为判定一个字符串的结尾,而是使用了独立的len,这样可以保证即使存储的数据中有'\0'这样的字符,它也是可以支持读取的.

引用[[@yudiandemingziTanTanRedisWuZhongShuJuJieGouJiZhenShiYingYongChangJingYuDianDeMingZiBoKeYuan]]所描述：
> String 类型是 Redis 中最基本、最常用的数据类型，甚至被很多玩家当成 Redis 唯一的数据类型去使用。String 类型在 Redis 中是二进制安全(binary safe)的,这意味着 String 值关心二进制的字符串，不关心具体格式，你可以用它存储 json 格式或 JPEG 图片格式的字符串。

重點：
- Redis 的String 本身是由原生字串改造的，並且本身定義為Binary Safe，這表示Redis上的String會以二進制來看待，不會以特定格式看待


## 複習
#🧠 Redis 面對String 會以Binary-safe來處理，這表示什麼？  ->->-> `表示Redis上的String會以二進制來看待，不會以特定格式看待`
<!--SR:!2022-06-20,10,250-->

---
Status: #🌱 
Tags:
[[String]] - [[Redis]]
Links:
[[Binary-Safe function 是指一個在處理二進制內容的過程中會以二進制來處理且不會以特殊格式來看待並進而破壞內容的函式]]
References:
[[@xiadayuErJinZhiAnQuanBinarySafe]]
[[@yudiandemingziTanTanRedisWuZhongShuJuJieGouJiZhenShiYingYongChangJingYuDianDeMingZiBoKeYuan]]