## 描述


### class-based component 的狀態
1. 以this.state來定義，且只能使用state這個名稱，不能依據喜歡來取名為任何名稱來代表狀態，這是因為state本身是React.Component類別下的屬性

2. state 在class-based component是React.Component的唯一能夠定義狀態的屬性，本身沒辦法像functional component那樣，每個狀態都擁有各自的定義方式和各自的更新用函式，必須得以物件形式來包含元件下的所有狀態，而每個屬性會是每個狀態：


#### 總結
class-bassed component 的狀態：
- 只能使用state、this.state來管理元件下的所有狀態和更新狀態
- state 通常是以物件來表示，單一值僅會在只有一個狀態才會出現

### functional componet 的狀態

1. 在functional component，由於每個狀態都可以註冊成各自的獨立狀態和狀態更新用函式
2. 由於狀態可以是獨立，不用以物件來囊括所有狀態，所以 state 通常是任意值






## 複習


---
Status: #🌱 #
Tags:
[[React]]
Links:
References: