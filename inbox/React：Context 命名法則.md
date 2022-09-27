## 描述


### 存放結構
每個Context會存放在/src/store目錄下，store是React世界用來儲存狀態的集中中心


### 每個context的名稱命名

檔案名稱會以要存放哪種功能下的狀態來命名：
- 功能名稱 + "-" +context + ".js"，比如說要儲存認證功能的狀態，那麼就是auth-context.js

### context 檔案內部
1. 定義Context.Provider來構建專門管理特定功能下狀態的元件並匯出元件
2. 單純建立context並匯出


## 複習

#🧠 React：每個context會存放在哪？以常見的用法來說 ->->-> `/src/store`

#🧠 React：每個專門儲存狀態的context會是什麼檔案？->->-> `JS`

#🧠 React：每個專門儲存狀態的context檔案會是什麼命名法則？ ->->-> `功能名稱 + "-" +context + ".js"`


#🧠 React：若以儲存認證功能的狀態為例，那麼其context檔案名稱為 ->->-> `就是auth-context.js`


#🧠 React：每個專門儲存狀態的context 會存哪種內容？ ->->-> `1. 定義Context.Provider來構建專門管理特定功能下狀態的元件並匯出元件 2. 單純建立context並匯出`


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: