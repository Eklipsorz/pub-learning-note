## 描述

### 不同點

#### CSS-in-JS 
Styled-Components 是 CSS-in-JS 概念的實現；CSS modules 則不是CSS-in-JS概念的實現

#### 元件樣式層面的渲染是否重複渲染

1. Styled-Components 由於是以JS角度將指定樣式內容寫進對應的Component ，所以只要觸發對應元件的渲染，都有可能間接讓styled-components元件重新解析樣式內容來決定最後對應內容

2. CSS modules 本身並不是將指定樣式內容寫進對應的Component，而是在經過webpack解析後，就讓載入的CSS 檔案所擁有的class selector重新以 新的selector名稱來命名，並且將使用CSS modules 語法的元件全替換成新selector名稱來使用對應原有的樣式屬性內容

總結：
- 前者會在執行下依據觸發渲染時所被給予的資訊來決定樣式內容，所以每次渲染觸發都會有成本
- 後者在一開始webpack的解析就決定好樣式內容，每一次渲染觸發都不能決定樣式內容，所以每次渲染觸發都不會有成本


#### JS和樣式體系

1. Styled-Components 是將CSS原生語法納入至JS上，並不會區分JS語法體系和CSS語法體系
2. CSS modules 是允許區分JS語法體系和CSS語法體系

#### css-preprocessor 
1. Styled-Components 由於是直接將CSS原生語法納入至JS，對於產出CSS原生語法的CSS preprocessor本身語法沒辦法全面性支援
2. CSS modules 是允許區分JS語法體系和CSS語法體系，所以CSS部分可以採用css preprocessor 來產生的CSS


### 相同點

#### 不論使用CSS-in-JS還是CSS modules，都是處於同個CSSOM

#### 都替特定樣式內容註冊一個獨特的class selector 名稱

## 複習

#🧠 Styled-Components 和 CSS modules 之間的相同點是什麼？ ->->-> `不論使用CSS-in-JS還是CSS modules，都是處於同個CSSOM、都替特定樣式內容註冊一個獨特的class selector 名稱`
<!--SR:!2023-07-09,192,250-->

#🧠 Styled-Components 和 CSS modules 之間的不同點為何？拿CSS-in-JS來說吧 ->->-> `Styled-Components 是 CSS-in-JS 概念的實現；CSS modules 則不是CSS-in-JS概念的實現`
<!--SR:!2023-07-11,194,250-->


#🧠 Styled-Components 和 CSS modules 之間的不同點為何？拿元件樣式層面的渲染是否重複渲染來詳細說明吧 ->->-> `Styled-Components 由於是以JS角度將指定樣式內容寫進對應的Component ，所以只要觸發對應元件的渲染，都有可能間接讓styled-components元件重新解析樣式內容來決定最後對應內容、CSS modules 本身並不是將指定樣式內容寫進對應的Component，而是在經過webpack解析後，就讓載入的CSS 檔案所擁有的class selector重新以 新的selector名稱來命名，並且將使用CSS modules 語法的元件全替換成新selector名稱來使用對應原有的樣式屬性內容`
<!--SR:!2024-03-09,336,250-->

#🧠 Styled-Components 和 CSS modules 之間的不同點為何？拿元件樣式層面的渲染是否重複渲染來簡答吧 ->->-> `Styled-Components在執行下依據觸發渲染時所被給予的資訊來決定樣式內容，所以每次渲染觸發都會有成本，CSS modules在一開始webpack的解析就決定好樣式內容，每一次渲染觸發都不能決定樣式內容，所以每次渲染觸發都不會有成本 `
<!--SR:!2024-10-06,461,250-->

#🧠 Styled-Components 和 CSS modules 之間的不同點為何？拿JS和樣式體系來說吧 ->->-> `Styled-Components 是將CSS原生語法納入至JS上，並不會區分JS語法體系和CSS語法體系、 CSS modules 是允許區分JS語法體系和CSS語法體系`
<!--SR:!2024-11-21,499,250-->


#🧠 Styled-Components 和 CSS modules 之間的不同點為何？拿css-preprocessor 來說吧 ->->-> `Styled-Components 由於是直接將CSS原生語法納入至JS，對於產出CSS原生語法的CSS preprocessor本身語法沒辦法全面性支援；CSS modules 是允許區分JS語法體系和CSS語法體系，所以CSS部分可以採用css preprocessor 來產生的CSS`
<!--SR:!2023-07-02,188,250-->


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References: