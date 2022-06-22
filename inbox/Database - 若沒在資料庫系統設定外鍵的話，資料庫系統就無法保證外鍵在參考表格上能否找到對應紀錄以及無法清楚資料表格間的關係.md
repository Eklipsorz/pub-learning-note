## 描述
[[@piotrkononowReasonsWhyThere]] 所描述：
> ## Why is that a problem?

> ### 1. Potential data integrity issues, duh
> The obvious problem with the lack of foreign keys is that a database can't enforce referential integrity and if it wasn't taken care of properly at the higher level then this might lead to inconsistent data (child rows without corresponding parent rows).

> ### 2. Tables relations are not clear
> Another, less visible, negative effect of lack of foreign keys in a database is that people who don't know the schema have a hard time finding the right tables and figuring out table relations. This may lead to [serious problems](https://dataedo.com/blog/2-common-sql-join-traps-with-test-queries) with querying and reporting from the database.


重點：若沒在資料庫系統設定外鍵的話
- 資料庫系統就無法保證外鍵在參考表格上能否找到對應紀錄
- 無法清楚知道資料表格間的關係，恐會讓程式在執行上誤解以及開發者在開發上的誤解來造成其他錯誤
- 反之，設定外鍵是確保外鍵能夠在參考表格找到對應紀錄 以及 清楚知道表格間的關係，以減少不必要誤解
- 另外，於資料庫系統上的外鍵和開發認知上的外鍵設計是可能不同的，比如不在資料庫系統設定外鍵，只是以認知上來表明哪些表格之間有何種關係以及哪裡可以參考和被參考

## 複習
#🧠 若沒在資料庫系統設定外鍵的話，會有哪兩種缺失發生(提示：我可以保證找得到參考資料嗎？若我是外人，我看得懂關係嗎) ->->-> `- 資料庫系統就無法保證外鍵在參考表格上能否找到對應紀錄 - 無法清楚知道資料表格間的關係，恐會讓程式、開發者誤解並造成其他錯誤`

#🧠 若沒在資料庫系統設定外鍵的話，會讓其他人無法清楚知道表格之間的關係，這樣子會發生什麼事情(提示對於開發上和系統維護上) ->->-> `恐會讓程式在執行上誤解以及開發者在開發上的誤解來造成其他錯誤`

#🧠 另外，於資料庫系統上的外鍵和開發認知上的外鍵設計可以是不同的嗎->->-> `可以，只是一個在資料庫系統強制告知關係和參照關係，另一個則是認知上的認同`

---
Status: #🌱 
Tags:
[[Database]]
Links:
[[Database - Referential integrity 是指一筆資料紀錄上的外鍵是否都能在原本參考到表格上找到對應的紀錄之特性]]
References:
[[@piotrkononowReasonsWhyThere]]
[[@postgresdexiaodaogushiYiZiLiaoKuZhongBuShiYongWaiBuJianDeGeLiYou]]