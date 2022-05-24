

## GCP 前置所需概念
- CIDR
[[一個主機發送封包的模式- unicast 1對1 broadcast 1對all multicast 1對多]]
[[CIDR 取代分類定址來實現子網域定義並彈性分配適當數量的IP給使用者]]
[[CIDR 可以讓多個網域根據共同所擁有的序號來合併成另一個網域來代表多個網域]]

- 分類定址
[[網路IP的子網域是從8位元演變至classful addressing]]
[[分類定址是將IP分個群組來重新定義使用者能用的IP群組是什麼]]

- IP
[[Network ID描述IP所屬的網域，Host ID描述主機在網域上的獨特序號]]
[[一個IP群組上一定會有負責用來識別整個IP群組以及廣播位址]]
[[以0或255結尾的位址不一定是識別用和廣播用的]]

- 遮罩
[[子網域的切分不只類別定址，主要由遮罩來決定]]


- Serverless
[[Serverless Computing 將對於伺服器本身的開發和管理 從開發抽離出來]]

- 虛擬雲
[[虛擬雲 或 虛擬網路 是以軟體形式來實現組成網路所需的儀器以及機制，從而組成虛擬網路]]

- Access Control List
[[ACL vs ACM 是差在定義權限的結構是不一樣]]
[[Access Control List 是使用串列來定義每個物件所擁有的權限]]

- Access Control Matrix
[[ACL vs ACM 是差在定義權限的結構是不一樣]]
[[Access Control Matrix 是用表格來定義每個使用者對於每個資源的存取權限]]

## 對外對內的服務
- 對外的服務
[[GCP serverless service 在一開始被建立後所處的網路能夠對外，但不是處於VPC]]
- 對內的服務
[[Compute engine VM 和 memoryStore會是在VPC內部的服務]]



## GCP 特定功能
- region & zone
[[GCP- region & zone，region 是指資料中心的所在地，泛指實際資料中心，zone會是指region的子區域，泛指實際資料中心的子資料中心]]

- cloud shell
[[cloud shell 可連線至指定專案下的Serverless Service主機]] 


- Cloud SQL
[[Cloud SQL 與客戶端之間的傳輸過程使用SSL來加密]]

- Google Cloud Storage 
[[使用Google cloud storage API來上傳檔案至storage平台上]]
[[Cloud Storage 是Google 用來儲存資料的雲端服務]] 
[[gcloudignore造成.env檔案無法正常上傳至app engine]]
[[gsutil 是用來遠端操控Cloud Storage的工具]]
[[讀取指定google storage bucket下的指定物件]]

- VPC
[[VPC 如同實體網路可以擁有屬於自己的子網域]]

- Serverless VPC access
[[Serverless VPC access connector 是轉遞無伺服器環境和指定VPC兩者之間的封包傳遞]]

- IAM
[[使用Google API必須透過建立對應權限的帳號並從中對應帳號的access-token(key)]]
[[Identity and Access Management 設定哪些使用者對哪些資料進行哪一種操作的許可]]
- MemoryStore
[[Google Cloud Memorystore 是以提供記憶體儲存空間為主的服務]]