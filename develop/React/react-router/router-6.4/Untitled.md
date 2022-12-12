## 描述


loader

> Each route can define a "loader" function to provide data to the route element before it renders.

  

loader 本身函式物件的參數是特定物件，該物件擁有request、params屬性，前者是從當使用者在客戶端透過URL切換向伺服器發送請求對應URL的頁面時，react-router會攔截該請求並由它負責產生對應URL的頁面，同時會將request轉換成物件來當作這裡的屬性，通常request物件會包含請求封包本身，比如說當使用者透過URL切換來藉此向伺服器索求對應URL的頁面，Router會攔截該請求，並由它幫忙轉換對應頁面。 而params屬性則是目前所處的route 元件所攔

截到的url parameters 參數部分

  

params 是物件，裡面夾雜了目前所處Route所攔截到的URL參數部分

```
1.  function loader(obj) {
2.  }

4.  obj = {
5.     params：  ...,
6.     request：....
7.  }
```

## 複習

---
Status: #🌱 
Tags:
[[React]]
Links:
References: