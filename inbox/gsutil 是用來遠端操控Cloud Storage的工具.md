What is acl?

  

https://zh.m.wikipedia.org/zh-tw/身份管理

  

gsutil is a Python application that lets you access Cloud Storage from the command lin

gsutil mb => means make buckets

gsutil acl =>  acl - Get, set, or change bucket and/or object ACLs

  

1.  Make buckets => 

gsutil mb -l asia [gs://belazy-shop](gs://belazy-shop)

  

gsutil defacl set public-read-write gs://[belazy-shop](gs://belazy-shop)

  

  

public-read-write

  

1.  创建存储分区。通常以项目 ID 命名存储分区（并非必需）。存储分区名称必须保持全局唯一。  
      
    gsutil mb gs://<your-bucket-name>
2.  设置 ACL，授予对存储分区中内容的读取访问权限。  
    gsutil defacl set public-read gs://<your-bucket-name>
3.  将内容上传到存储分区。rsync 命令通常是上传和更新资源最快速、最便捷的方法。此外，您也可以使用 cp。  
    gsutil -m rsync -r ./static gs://<your-bucket-name>/static
4.    
    

NAME

  defacl - Get, set, or change default ACL on buckets
	
	
	
---
Status: #📥 
Tags:
[[GCP]]
Links:
[[Cloud Storage 是Google 用來儲存資料的雲端服務]] - [[Access Control List 是使用串列來定義每個物件所擁有的權限]]
References:
