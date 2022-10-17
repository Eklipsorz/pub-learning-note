## 描述






載入時遇到錯誤時所會有的處理和渲染：

- 先註冊狀態來表示是否有錯誤

`const [error, setError] = useState(null)`

- 在處理載入資料的程式模組前面添加重置錯誤的手段，確保每一次畫面渲染都會按照是否正確來呈現
```
setError(null)
// 處理載入資料
```

- 在處理載入資料的程式模組中的攔截錯誤部分添加，另外記得添加setIsLoading(false)保證按照實際情況來呈現預期效果
```
setError(error.message)
setIsLoading(false)
```

- 渲染部分則根據錯誤是否存在而呈現

  

  

如果載入中遇到錯誤的話，就應該會將狀態：

- isLoading: true -> false (設定是為了避免預期外的錯誤)

- error: false -> true

even if we have an error, we're not loading anymore

  

  
### 向伺服器發送請求的API是否會把夾雜錯誤狀態碼的回應物件視為真正的錯誤
  

one problem we'll face here is that the Fetch API doesn't treat error status codes as real errors

-> Fetch API 並不會把夾雜錯誤狀態碼的回應物件視為真正的錯誤

  

axios API 會把夾雜錯誤狀態碼的回應物件視為真正的錯誤

  

解決方式為：

- 在try block中添加判斷狀態碼是否為錯誤代碼而手動拋錯

if (!response.ok) {
 throw new Error(...)
}


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: