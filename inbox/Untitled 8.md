## 描述

### reload react app 的後果
- 失去整個app的目前所有DOM
- 失去整個app的目前所有狀態、Effect、Hook



### 表格輸入欄值存取方式

- 使用change事件 ＋ state：使用state來替代輸入欄位的value屬性(attribute)，並於事件處理那邊使用setState來攔截資訊至state
- 使用ref ：使用DOM節點所擁有的value來存取



### 輸入欄存取適用場景


> how do you decide which one to use?
> it depends what you plan to do with the entered value.

>- if you are only interested in it once when the form is submitted ：a ref might be better because logging and updating the state value with every keystroke is a bit overkill then.

> - if you of course need value, the entered value after every keystroke, e.g., for instant validation：state

> another reason for using a state instead of a ref could be,  if you want to reset the enter input




重點：
- refs 為主或者DOM API來擷取輸入欄 是適用於 
	- **針對提交時或者特定時間點時所擁有的資訊來處理**
- React 體系的state + setState 是適用於 
	- **針對每次使用者所輸入(每次鍵盤敲擊時)的內容來處理** ，如需要即時根據內容來顯示內容驗證結果
	- 方便從React體系下的語法來管理元件的狀態，如重設輸入欄的value，就可以透過setState來實現

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: