

reply 路徑選擇

## 需求
1. 可以讀取任意產品下的留言
2. 可以刪除對應留言
3. 可以編輯對應留言
4. 可以新增留言


### 設計一：
完全採用
```
/replies/:productId 
```


```
// 讀取對應產品的所有留言
GET /replies/:productId 

// 建立對應產品的留言
POST /replies/:productId

// 刪除對應產品的留言
DELETE /replies/:productId

// 編輯對應產品的留言
PUT /replies/:productId
```

缺點：
- 無法直接指定留言來處理，一切只能依據著邏輯設計來決定
- 有點不符合REST設計

優點：
- 可以減少實作上所需的檢測- 檢查目前留言是否屬於自己的

### 設計二：
一部分採取
```
/products/:productId/replies
```

```
// 讀取指定產品下的所有留言
GET /products/:productId/replies

// 在指定產品下新增留言
POST /products/:productId/replies
```

另一部分採取

```
/replies/:replyId
```

```
// 刪除指定留言
DELETE /replies/:replyId

// 編輯指定留言
PUT /replies/:replyId

// 瀏覽指定留言
GET /replies/:replyId
```

缺點：
- 實際業務邏輯要另外切分才能切出專門處理留言部份的業務邏輯，且能夠包含讀取指定產品下的所有留言和在指定產品下新增留言


優點：
- 更符合REST 設計

---
Status: #📥 
Tags:
Links:
References: