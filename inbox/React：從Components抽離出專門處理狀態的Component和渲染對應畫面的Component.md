## 描述

for better IDE auto-completion.

1. 會事先在createContext中的defaultValue設定未來會用到的資料型別是什麼，好讓IDE能夠更好地補全程式碼，比如當寫下ctx.時，IDE會判斷ctx會有什麼屬性

2. 型別若是函式且沒引數，就設定dummy function，形式會是：
`onLogout: () => {}`

3. 型別若是函式且有引數，就設定dummy function，形式會是：
`onLogin: (email, password) => {}`



### 從Components抽離出專門處理狀態的Component和渲染對應畫面的Component


專門處理狀態的Component 會以對應Context的Provider Component為主來構築，其Component會夾雜著與Context相關的狀態、更新用函式、Effect

被抽離之後，Component就保有渲染對應元件畫面的職責，Provider Component就維持著負責狀態管理的職責



#### 目的
1. 實現單一職責原則(Single responsibility principle)


### Single responsibility principle 

[[@freecodecampSOLIDDefinitionSOLID2022]]
> ## The Single Responsibility Principle (SRP)
> The idea behind the SRP is that every class, module, or function in a program should have one responsibility/purpose in a program. As a commonly used definition, "every class should have only one reason to change".


重點：
- 每一個類別、模組、函式都只會有一個職責或者單一目的來開發


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@freecodecampSOLIDDefinitionSOLID2022]]