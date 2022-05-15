## 描述


分類定址原文為 **Classful Addressing**，具體作法會是使用網路遮罩[[網路遮罩是用來判斷目前IP所屬的子網域是什麼]]的技術初步將IP分為三類的IP群組：
	
```
Class A: 0.0.0.0 ~ 127.
Class B:
Class C:
```


[[@lokeshgallaIPv4ClassesRanges]]

![](https://www.researchgate.net/profile/Lokesh-Galla/publication/260622269/figure/fig1/AS:340713477820416@1458243831010/1-1-IPv4-Classes-Ranges.png)

https://zh.m.wikipedia.org/wiki/%E5%88%86%E7%B1%BB%E7%BD%91%E7%BB%9C

&

11111001  => 11111001

  實際在子網域下的IP，用1對應出該IP對應的子網域，沒遮擋的數字則是實際該子網域的位置


將IP分成8、16、24位元並分為ABC類別這三類

  

  

子網路遮罩的好處就是：不管網路有沒有劃分子網路，只要把子網路遮罩和IP位址進行逐位的「與」運算（AND）即得出網路位址來。這樣在路由器處理到來的分組時就可以採用同樣的方法


## 複習

---
Status: #🌱 
Tags:
[[Network]]
Links:
[[網路遮罩是用來判斷目前IP所屬的子網域是什麼]]
References:
[[@wikidataZiWangYu2021]]
[[@lokeshgallaIPv4ClassesRanges]]