## 描述





Link 和 NavLink 本身在v6並沒有太大的改變，主要改變的點是NavLink上的activeClassName屬性：

v6 是

1. 直接移除activeClassName

2. 直接以className來接收一個會回傳class name的函式物件，其參數會由react-router所提供的navigation 狀態物件，其中有個屬性(property)為isActive，屬性值為布林值，當目前NavLink為active element，isActive為ture；否則為false

###
useParams 用法沒變動

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router v6：從多個路徑挑選一個路徑和Route 語法之間的改變]]
References: