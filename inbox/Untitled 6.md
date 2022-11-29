## 描述

### 增加特定Quote的評論所需的quoteId

																											若元件本身
/quotes/:quoteId/xxxx 頁面元件下，可使用以下方法來獲取quoteId

1. 使用useParams來擷取quoteId：考量到元件不一定會在路徑為/quotes的Route內，若貿然添加會使該元件的可重複率變低。

> we can't embed it anyway else in the page, where the url might not include that quoteId

2. 使用props.quoteId：可提昇可重複使用

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: