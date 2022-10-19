
## 描述


### 開發custom hook的注意事項

custom hook ：
- 通常會將hook function 以一個單一檔案來儲存，檔名通常會取use-xxxx.js，xxxx為功能名
- hook function 放置在/src/hooks




### 定義custom hook的條件


[[@reactBuildingYourOwn]]
> **A custom Hook is a JavaScript function whose name starts with ”`use`” and that may call other Hooks**

1. 必須是function
2. function 名稱必須要是use 開頭：當被設定時，react會開始檢查其他條件是否滿足成為hook的條件


若不滿足的話，會被當作一般函式看待。


### setInterval() 用法

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
[[React]]
Links:
References:
[[@reactBuildingYourOwn]]
[[@mdnSetIntervalWebAPIs]]





