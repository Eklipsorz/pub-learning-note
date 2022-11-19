## 描述




### react-router 所提供的 history.push & replace
1. 若每一次對stack的最上面元素做push或replace，會針對切換前後的畫面之間差異來切換，而非單方面使react執行一次unmount 和 一次mount




#### 若一直push或者replace相同頁面所帶來些許效能浪費
1. 即使是一直push相同頁面的網址，會因為本身會有執行render的成本、比較成本，但卻因為結果都會是一樣而呈現是浪費




## 複習

#🧠 react-router 所提供的 history.push & replace，會不會每一次對stack的最上面元素做push或replace，而產生unmount和mount？為什麼？->->-> `並不會，每一次對stack的最上面元素做push或replace，會針對切換前後的畫面之間差異來切換`
<!--SR:!2022-11-22,3,250-->

#🧠 react-router 所提供的 history.push & replace，若對stack的最上面元素做push或replace，所產生的切換會是？->->-> `每一次對stack的最上面元素做push或replace，會針對切換前後的畫面之間差異來切換`
<!--SR:!2022-11-22,3,250-->


---
Status:  #🌱 
Tags:
[[React]]
Links:
[[react-router-practice：使用useHistory來實現programmatic navigation，具體會是操縱瀏覽器的瀏覽紀錄來進行]]
References: