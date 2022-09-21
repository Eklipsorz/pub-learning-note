## 描述

> important rule regarding this HTML
> one parent node per a return statement / per JSX code snippet



1. 每一個React Elemenet的內容只會允許一個parent 節點

  

錯誤案例為如下，首先以下有兩個parent 節點，一個為有Date的div標籤，另一個為有h2標籤的div標籤。
```
return (  
   <div>Date</div>  
   <div><h2>...</h2></div>  
)
```

  

why is that not allowed

## 複習
#🧠 React：請問我可以在每一個React element放置多個parent 節點嗎？為什麼 ->->-> `不能，因為每一個React Elemenet的內容只會允許一個parent 節點`
<!--SR:!2022-12-04,74,250-->

#🧠 React：請問React Element設定如下，能正常執行嗎？ 為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660149890/blog/react/react-element/wrong-react-element_ih5rsf.png) ->->-> `不能，以下有兩個parent 節點，一個為有Date的div標籤，另一個為有h2標籤的div標籤。然而每一個React Elemenet的內容只會允許一個parent 節點`
<!--SR:!2022-11-24,67,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: