


## 描述


### upper camel case
[[@wikidataTuoFengShiDaXiaoXie2022]] 所描述：
> 單字之間不以空格斷開（例：camel case）或連接號（-，例：camel-case）、底線（_，例：camel_case）連結，有兩種格式：
> - 小駝峰式命名法（lower camel case）： 第一個單字以小寫字母開始；第二個單字的首字母大寫，例如：firstName、lastName。
> - 大駝峰式命名法（upper camel case）： 每一個單字的首字母都採用大寫字母，例如：FirstName、LastName、CamelCase，也被稱為Pascal命名法（英語：Pascal Case）。

重點：
- camel case 是一種命名資料的命名法，會是單字間不以任何字元符號隔開，直接接在一起
- camel case 根據每個單字的首字是否一定要大寫而區分：
	- Upper Camel Case：每一個單字的首字母都是大寫，剩下皆為小寫，如FirstName、LastName
	![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/CamelCase.svg/250px-CamelCase.svg.png)
	- Lower Camel Case：除了第一個單字都是小寫以外，剩下的每個單字下的首字母都是大寫，剩下皆為小寫，如：firstName、lastName
![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/CamelCase.png/250px-CamelCase.png)
### Component 命名方式
[[React Componet 傳統命名是以upper camel case，且App.js會是主要Virtual DOM中的根節點]]

代表對應Component 的函式名稱會是upper camel case來命名

### Component 檔案名稱 命名方式
React Component 檔案名稱會是以upper camel case來命名

### React Element的attributes命名方式
React Component在標籤上的屬性(attributes)命名方式為lower camel case

### React Element上的事件綁定callback名稱

若沒特別命名法則來命名每個事件綁定的callback，那麼可以試著以 xxxx + Handler 來命名，其中xxxx為事件名稱。
```
const clickHandler = () => {
	.....
}
```

畢竟

## 複習
#🧠 camel case 是什麼？->->-> `camel case 是一種命名資料的命名法，會是單字間不以任何字元符號隔開，直接接在一起`
<!--SR:!2022-11-01,49,250-->

#🧠 camel case 根據什麼而區分成Upper Camel Case 和 Lower Camel Case ->->-> `根據每個單字的首字是否一定要大寫而區分`
<!--SR:!2022-11-03,50,250-->

#🧠 Upper Camel Case 是怎麼樣的命名法？ ->->-> `每一個單字的首字母都是大寫，剩下皆為小寫`
<!--SR:!2022-09-26,28,250-->


#🧠 請試著用lastname來舉一個upper camel case的例子？ ->->-> `LastName`
<!--SR:!2022-11-06,52,250-->

#🧠 Lower Camel Case 是怎麼樣的命名法？->->-> `除了第一個單字都是小寫以外，剩下的每個單字下的首字母都是大寫，剩下皆為小寫`
<!--SR:!2022-09-26,28,250-->

#🧠 請試著用lastname來舉一個lower camel case的例子？ ->->-> `lastName`
<!--SR:!2022-12-09,74,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@wikidataTuoFengShiDaXiaoXie2022]]