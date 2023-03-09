## 描述




### 抽離出向後端發出的請求業務邏輯
前端優化方向可以是從以下方向來抽離出向後端發出的請求業務邏輯：
- 元件上的渲染層面
- 元件上的業務邏輯

將抽離出來的請求業務邏輯存放至以下目錄：
```
/src/lib
```


#### 範例

```
const FIREBASE_DOMAIN = xxxxx;

export async function getAllQuotes(...) {...}
export async function addQuote(...) {...}
.
.
.
```


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: