
## 描述

[[@mdnSetIntervalWebAPIs]]
> The setInterval() method, offered on the Window and Worker interfaces, repeatedly calls a function or executes a code snippet, with a fixed time delay between each call. 

```
setInterval(func, delay)
```

重點：
- setInterval 產生一個非同步計時任務，該任務會按照delay給予的秒數來自動生成一個非同步任務
- 任務內容會以func為主
- 任務數會一直產生，不會停止，除非手動停止

## 複習

---
Status: #🌱 
Tags:
Links:
References:
[[@mdnSetIntervalWebAPIs]]





