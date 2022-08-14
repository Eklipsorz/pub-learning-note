## 描述



### 將component 當函式呼叫並回傳對應畫面
為了要將component 當作函式來呼叫，並用資料當參數，直接將資料輸入至函式就能產生出對應資料的畫面，在react會使用props概念來實現


#### 初始想法
一般來說，會於**在App元件上的JS宣告一個變數A，並將變數A放置在App元件下的元件A上來顯示的話，若沒特別處理，是無法將變數A傳遞過去**


#### 解法
1. 使用props概念：
> 將component當作標籤來使用，並對該標籤添加對應屬性值(attributes)，對應component的函式會以物件形式來存放這些屬性值(attributes)，而這些物件的每一個屬性(property)皆為原本的屬性(attribute)，因此被稱之為properties或者props

2. props 傳遞形式：對代表指定元間的標籤設定屬性名稱和屬性值(attribute)，比如CourseGoalItem標籤被賦予title、amount、date這三個屬性，而屬性值分別為title1、amount1、date1
```
<CourseGoalItem title=title1 amount=amount1 date=date1 />
```
3. props 接收形式為：在對應component的function以物件來當參數接收所有attributes，每一個物件上的屬性(property)名稱皆對應著傳過來的屬性attribute名稱，其值根據屬性名稱來設定

寫法1：按照attribute名稱來對應變數名稱並賦予 (這方法會被react阻止)
```
function CourseGoalItem(title, amount, date) {
     // ......
}
```
寫法2：若以一個參數來寫，就會以物件形式來存放所有attributes，其屬性名稱會按照attribute名稱來填寫，而attribute值則是按照對應值來賦予對應屬性值(property)
```
function CourseGoalItem(data) {
    // ......
}
```


寫法3：若以一個參數來寫，就會以物件形式來存放所有attributes，其屬性名稱會按照attribute名稱來填寫，而attribute值則是按照對應值來賦予對應屬性值(property)
```
function CourseGoalItem(props) {
    // ......
}
```

4. 在對應元件的函式善用{}和expression關係就能將從標籤獲取到來的attributes進行善用

[[React：資料和畫面的切分第一步驟是用{}以及在其內部JavaScript表達式來切分]]





### props 具體是


這裡的Component 會是由function所建立的
```
<Component attribute1=value1 attribute2=value2 ...>Content</Component>
```

原本在這裡所賦予的attributes會被存放在名為props的物件上，其屬性(property)名稱和值會按照attribute名稱和其值而對應，並且在React上會被是作為該Component 物件上所擁有的屬性
```
function Component(props) {
	// ....
}
```

## 複習
#🧠 React：為了要讓component能夠因為資料的不同而有所不同，初步想會是什麼？->->-> `為了要將component 當作函式來呼叫，並用資料當參數，直接將資料輸入至函式就能產生出對應資料的畫面`
<!--SR:!2022-08-24,10,250-->

#🧠 React：為了要將component 當作函式來呼叫，並用資料當參數，直接將資料輸入至函式就能產生出對應資料的畫面，解法會是？(描述概念) ->->-> `使用props概念`
<!--SR:!2022-08-24,10,250-->


#🧠 在代表特定元件A的特定函式中，其參數props對於其元件A會是代表什麼？ ->->-> `props會是被視作為元件物件A的屬性(properies)`
<!--SR:!2022-08-17,3,250-->

#🧠 React：請問props概念是什麼？ ->->-> `將component當作標籤來使用，並對該標籤添加對應屬性值(attributes)，對應component的函式會以物件形式來存放這些屬性值(attributes)，而這些物件的每一個屬性(property)皆為原本的屬性(attribute)，因此被稱之為properties或者props`
<!--SR:!2022-08-24,10,250-->

#🧠 React：請問透過props來傳遞資料至component的形式為？ ->->-> `對代表指定元間的標籤設定屬性名稱和屬性值(attribute)，<Component attribute1=value1 ..../> 或者<Component attribute1=value1 .....> <Component />`
<!--SR:!2022-08-24,10,250-->

#🧠 React：假設要傳入title=title1、amount=amount1、date=date1 給CourseGoalItem這自製的component，如何用代碼來表示->->-> `<CourseGoalItem title=title1 amount=amount1 date=date1 />`
<!--SR:!2022-08-15,3,250-->


#🧠 React：請問從component如何接收到attributes來當參數？ ->->-> `在對應component的function以物件來當參數接收所有attributes，每一個物件上的屬性(property)名稱皆對應著傳過來的屬性attribute名稱，其值根據屬性名稱來設定`
<!--SR:!2022-08-24,10,250-->

#🧠 React：請問從component如何接收到attributes來當參數？以代碼來表示 ->->-> `function CourseGoalItem(data) {....}或者function CourseGoalItem(props) {...}，接著在以props的屬性來取用對應的attribute值`
<!--SR:!2022-08-24,10,250-->

#🧠 React：function CourseGoalItem(title, amount, date)可以接收到賦予CourseGoalItem標籤的title屬性、amount屬性、date屬性嗎？->->-> `不能`
<!--SR:!2022-08-24,10,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：資料和畫面的切分第一步驟是用{}以及在其內部JavaScript表達式來切分]]
References: