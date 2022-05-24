

## 描述

ACL 是 Access Control List 的縮寫，以鏈結串列(linked list)來定義在特定系統上，特定物件A對於特定資源B的存取權限，首先：
- 賦予每個特定物件一個串列，一開始會是空串列(毫無節點)
- 假若一開始是空串列，那麼當特定物件對於特定資源是有存取權限時，就建立節點並標記哪個資源以及特定物件對於該資源的存取權限是為何，並定義串列的頭為該節點
- 假若一開始存在其他節點，那麼那麼當特定物件對於特定資源是有存取權限時，就建立節點Node，串列上的尾部節點就與該節點Node連接


範例：以下圖為例，假若在特定系統存在著三個特定物件s1、s2、s3能夠存取資源，而資源會有f1、f2、f3、f4、f5、f6，在這裡會先定義s1這物件對f2、f3的存取權限是有 **擁有者、讀取、寫入**這些權限，且對於f5的存取權限只有 **寫入** 這權限。 那麼在ACM[[Access Control Matrix 是用表格來定義每個使用者對於每個資源的存取權限]]中會是如下圖的表格上顯示，其中s1對於f1、s1對於f4、s1對於f6的欄位值會是空白，表示沒任何權限。

若改以ACL來顯示的話，那麼就會以該物件能夠存取的資源為主，也就是會f2、f3、f5：
	- 一開始會是空串列，而要建立s1對於f2的存取權限時，就會建立一個節點來標記orw以及f2這資源，而由於目前串列毫無節點，所以直接拿這新節點當作串列的頭
	- 接著當要建立s1對於f3的存取權限時，就會建立一個節點來標記orw以及f3這資源，接著拿串列最尾部的節點來與新節點串接，也就是拿f2節點去與f3節點串接
	- 接著當要建立s1對於f5的存取權限時，就會建立一個節點來標記w以及f5這資源，接著拿串列最尾部的節點來與新節點串接，也就是拿f3節點去與f5節點串接
![](https://www.researchgate.net/profile/James-Joshi/publication/27233516/figure/fig1/AS:638408414220289@1529219835691/An-access-control-matrix-and-its-access-control-list-and-capability-list.png)

note: 
1. 圖片是以[[@jamesb.d.joshiAccessControlMatrix]]為主
## 優點
1. 節省空間成本：可根據實際對於資源的存取權限需求來定義特定物件對於特定資源的權限，而非像ACM那樣會有固定成本在那


## 缺點
1. 要查詢特定物件對於特定資源時得遍歷整個串列才有可能查詢得到


## 複習
#🧠 Access Control List 是什麼？ ->->-> `ACL 是 Access Control List 的縮寫，以鏈結串列(linked list)來定義在特定系統上，特定物件A對於特定資源B的存取權限`
<!--SR:!2022-05-21,3,250-->

#🧠 Access Control List：試著用這張圖說明s1對於資源的權限 ![](https://www.researchgate.net/profile/James-Joshi/publication/27233516/figure/fig1/AS:638408414220289@1529219835691/An-access-control-matrix-and-its-access-control-list-and-capability-list.png)  ->->-> `以下圖為例，假若在特定系統存在著三個特定物件s1、s2、s3能夠存取資源，而資源會有f1、f2、f3、f4、f5、f6，在這裡會先定義s1這物件對f2、f3的存取權限是有 **擁有者、讀取、寫入**這些權限，且對於f5的存取權限只有 **寫入** 這權限。 那麼在ACM中會是如下圖的表格上顯示，其中s1對於f1、s1對於f4、s1對於f6的欄位值會是空白，表示沒任何權限。  若改以ACL來顯示的話，那麼就會以該物件能夠存取的資源為主，也就是會f2、f3、f5`
<!--SR:!2022-06-03,10,250-->


#🧠 Access Control List  優點為->->-> `節省空間成本：可根據實際對於資源的存取權限需求來定義特定物件對於特定資源的權限，而非像ACM那樣會有固定成本在那
<!--SR:!2022-06-06,13,250-->
`

#🧠 Access Control List  缺點為->->-> `要查詢特定物件對於特定資源時得遍歷整個串列才有可能查詢得到`
<!--SR:!2022-06-02,9,250-->

---
Status: #☀️  
Tags:
[[Operating System]]  - [[Array]] - [[LinkedList]]
Links:
[[Access Control Matrix 是用表格來定義每個使用者對於每個資源的存取權限]]
References:
[[@jamesb.d.joshiAccessControlMatrix]]