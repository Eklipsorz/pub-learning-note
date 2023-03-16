
## 描述


### API端點名稱是以多個英文單字組成的話

可以將多個單字拆分成獨立的單字並以特定符號或者形式來區隔開來，主要有：
1. Snake Case：單字間使用下底線來相連
2. Camel Case：單字間不用任何符號，而是以單字的首字為大寫，其餘則為小寫，但根據第一個單字的首字是否為大寫而區分為Lower Camel Case以及Upper Camel Case
3. Spinal Case：單字間使用連字號來相連
4. Dot Notation Case：單字間使用點字號來相連


#### 範例
以下面使用者的user timeline端點為範例

```
使用者：
http://api.example.com/v1/users/12345/
```

```
user timeline 端點 xxxxxxxx：
/statuses/xxxxxxx
```

#####  Snake Case
```
http://api.example.com/v1/users/12345/statuses/user_timeline
```


##### Spinal case
```
http://api.example.com/v1/users/12345/statuses/user-timeline
```


##### Camel Case
```
http://api.example.com/v1/users/12345/statuses/userTimeline
```

##### Dot Notation Case
```
http://api.example.com/v1/users/12345/statuses/user.timeline
```


## 複習

#🧠 API端點名稱是以多個英文單字組成的話，要怎麼做才能使端點更容易讓人類讀取？其概念為 ->->-> `將多個單字拆分成獨立的單字並以特定符號或者形式來區隔開來將`


#🧠 API端點名稱是以多個英文單字組成的話，可以使用什麼方法來將多個單字拆分成獨立的單字並以特定符號或者形式來區隔開來 ->->-> `Snake Case、 Camel Case、Spinal Case、 Dot Notation Case`

#🧠 Snake Case 是什麼樣的命名法則 ->->-> `單字間使用下底線來相連`

#🧠 Camel Case 是什麼樣的命名法則 ->->-> `單字間不用任何符號，而是以單字的首字為大寫，其餘則為小寫，但根據第一個單字的首字是否為大寫而區分為Lower Camel Case以及Upper Camel Case`


#🧠 Spinal Case 是什麼樣的命名法則 ->->-> `單字間使用連字號來相連`

#🧠 Dot Notation Case 是什麼樣的命名法則 ->->-> `單字間使用點字號來相連`


#🧠 以下面使用者的user timeline端點為範例 `http://api.example.com/v1/users/12345/`  來用Snake Case命名->->-> `http://api.example.com/v1/users/12345/statuses/user_timeline`

#🧠 以下面使用者的user timeline端點為範例 `http://api.example.com/v1/users/12345/`  來用Spinal Case命名->->-> `http://api.example.com/v1/users/12345/statuses/user-timeline`


#🧠 以下面使用者的user timeline端點為範例 `http://api.example.com/v1/users/12345/`  來用Lower Camel Case命名->->-> `http://api.example.com/v1/users/12345/statuses/userTimeline`


#🧠 以下面使用者的user timeline端點為範例 `http://api.example.com/v1/users/12345/`  來用Upper Camel Case命名->->-> `http://api.example.com/v1/users/12345/statuses/UserTimeline`


#🧠 以下面使用者的user timeline端點為範例 `http://api.example.com/v1/users/12345/`  來用Dot Notation Case命名->->-> `http://api.example.com/v1/users/12345/statuses/user.timeline`


---
Status: #🌱 
Tags:
[[API]] - [[API Design]]
Links:
References: