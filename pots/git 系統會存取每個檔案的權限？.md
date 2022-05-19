


## 描述

預設上來說，git系統會替每個版本下的每個檔案定義它們的權限，以便讓他們在從物件型態轉換成檔案系統下的檔案能有個正確權限能夠存取他們，通常只有：
- owner：能有rwx權限
- user & group：只能設定rx這兩個權限。

### 範例：
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


## note
git ls-files 呈現目前GIT工作目錄下的所有檔案，包含目前在暫存區的檔案。

git ls-files 參數
```
git ls-files --stage 呈現檔案被暫存內容

Show staged contents' mode bits, object name and stage number in the output.
```


---
Status: #🌱 
Tags:
[[Git]]
Links:
References:
[[@chienweichihJiuMingWoDeDangAnBeiGit]]