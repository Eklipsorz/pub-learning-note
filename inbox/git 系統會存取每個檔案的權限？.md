


## 描述

```

[feat/add-reply-service 74bf556] feat: add getReplies function
 7 files changed, 75 insertions(+), 1 deletion(-)
 create mode 100644 routes/modules/reply.js
 create mode 100644 services/resources/reply.js
 ```
 
 
 觀察reply.js權限
```
create mode 100644 routes/modules/reply.js
```

下達ls 去查同樣檔案的權限，也是644
```
-rw-r--r--  1 eklipsorz  staff  160  5 16 20:17 routes/modules/reply.js
```

或許版控系統會存取？

## note
git ls-files 呈現目前GIT工作目錄下的所有檔案，包含目前在暫存區的檔案。

git ls-files 參數
```
git ls-files --stage 呈現檔案被暫存內容

Show staged contents' mode bits, object name and stage number in the output.
```

git add
1. 將檔案/目錄設定成staged，並複製至staging area中
---
Status: #📥 
Tags:
[[Git]]
Links:
References: