## 描述


若在自製Component標籤上添加無屬性(attribute value)值的屬性名稱(attribute)的話，
```
<Component attr1 />
```

會被React改成如下
```
<Component attr1=true />
```

## 複習

#🧠 若在自製Component標籤上添加無屬性(attribute value)值的屬性名稱(attribute)的話，比如\<Component attr1 \/\>，Component1 的props會收到什麼？ ->->-> `會是true`
<!--SR:!2022-11-14,9,250-->

#🧠 若在自製Component標籤上添加無屬性(attribute value)值的屬性名稱(attribute)的話，比如\<Component attr1 \/\>，Component1 的props會收到true，為什麼？ ->->-> `若在自製Component標籤上添加無屬性(attribute value)值的屬性名稱(attribute)的話，<Component attr1 /> 會被React 修改成 <Component attr1=true />`
<!--SR:!2022-11-05,3,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: