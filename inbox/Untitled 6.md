## 描述


正解檔資源記錄 (resource record, RR) 格式

1.  Resource record 是用來解析對應域名為哪個域名和哪個IP
2.  在DNS Zone files中，是基本對應單位

  

A resource record, commonly referred to as an RR, is the unit of information entry in DNS zone files; RRs are the basic building blocks of host-name and IP information and are used to resolve all DNS queries

@

這個符號代表 zone 的意思！例如寫在 named.centos.vbird 中，@ 代表 centos.vbird.，如果寫在 named.192.168.100 檔案中，則 @ 代表 100.168.192.in-addr.arpa. 的意思 (參考 named.conf 內的 zone 設定)

(DNS) **zone file**

1.  描述**DNS Zone**
2.  一個**DNS Zone**：所有域名會由以域名的相同部分字串來分類，其每個類別皆為**DNS Zone**

  

  

-   從主機名稱查詢到 IP 的流程稱為：正解
-   從 IP 反解析到主機名稱的流程稱為：反解
-   不管是正解還是反解，每個領域的記錄就是一個區域 (zone)

舉例來說，崑山科大 DNS 伺服器管理的就是 *.ksu.edu.tw 這個領域的查詢權，任何想要知道 *.ksu.edu.tw 主機名的 IP 都得向崑山科大的 DNS 伺服器查詢，此時 .ksu.edu.tw 就是一個『正解的領域』。而崑山科大有申請到幾個 class C 的子網域， 例如 120.114.140.0/24，如果這 254 個可用 IP 都要設定主機名稱，那麼這個 120.114.140.0/24 就是一個『反解的領域』！ 另外，每一部 DNS 伺服器都可以管理多個領域，不管是正解還是反解。

## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-12-14,3,250-->

---
Status: #🌱 
Tags:
[[DNS]]
Links:
[[Canonical Name 在域名系統中的用途是以CName Record形式來記錄並且解析所有客戶端傳遞過來的域名名稱成它們真正的域名]]
References: