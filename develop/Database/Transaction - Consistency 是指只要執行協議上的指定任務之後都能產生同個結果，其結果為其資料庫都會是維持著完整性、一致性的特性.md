

## 描述



[[@wikidataACID2022]] 所描述的：
> Consistency ensures that a transaction can only bring the database from one valid state to another, maintaining database invariants: any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is _correct_. 


重點：
- Consistency 是指只要執行協議上的指定任務之後都能產生同個結果，其結果為其資料庫上的資料都會是維持著合法的特性
	- 合法是指滿足資料庫對於資料上的規則
- Consistency 提出目的是為了確保協議上的指定任務不破壞資料庫本身的一致性和完整性，但不一定保證著指定任務的結果都會如同開發者所要達成的目標
>  This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is _correct_.
-  Consistency 不一定就實現在每個協議，具體還要看資料庫系統是否支援和開發者是否添加特定語法

### consistency 命名緣由

[[@cambridgedictionaryConsistencyTranslateTraditional]] 所描述的：
> the quality of always behaving or performing in a similar way, or of always happening in a similar way

consistency 中文翻譯為一致性
[[@guojiajiaoyuyanjiuyuanGuoJiaJiaoYuYanJiuYuanShuangYuCiHuiXueShuMingCiJiCiShuZiXunWang]]所描述：
> #### 當某個現象發生後，如果再次提供與該現象發生時相彷的條件與情境時，類似的現象也會再度發生



重點：
- 第一部分指的是多個以同個情境和狀態發生或者類似的事件或者多個執行同個任務內容或者類似內容的任務之效果之間的相似性，若這些重複發生的發生的結果近似的話，代表相似度高；若這些執行多個同個任務內容的任務，其結果會是一樣的話，那麼相似度高，同時代表著一致性也跟著高
- 第二部分則是以consistency 翻過來的一致性來解釋其意思，但其一致性原文是 Uniformity
- 一致性在資料庫的Transaction是形容執行transaction 後都能產生某個結果 -其結果就是資料庫表格都能保持在一致性、完整性的

## 複習
#🧠 Consistency 原意為何？ (多個發生事件？是否一樣？如何一樣，其結果相似度為何？) ->->-> `多個以同個情境和狀態發生或者類似的事件或者多個執行同個任務內容或者類似內容的任務之效果之間的相似性，若這些重複發生的發生的結果近似的話，代表相似度高；若這些執行多個同個任務內容的任務，其結果會是一樣的話，那麼相似度高，同時代表著一致性也跟著高`
<!--SR:!2024-04-14,283,230-->


#🧠 Consistency 在 Transaction 所要表達什麼？ (請強調同個結果)->->-> `Consistency 是指只要執行協議上的指定任務之後都能產生同個結果，其結果為其資料庫上的資料都會是維持著合法的特性性`
<!--SR:!2024-06-29,361,250-->


#🧠 Consistency 加入至Transaction 是為了什麼？ ->->-> `Consistency 是指只要執行協議上的指定任務之後都能產生同個結果，其結果為其資料庫上的資料都會是維持著合法的特性`
<!--SR:!2024-06-28,358,250-->



#🧠 Consistency 加入至Transaction能夠確保transaction執行正確嗎？ 或者確保如同開發者那樣預期的結果嗎？ ->->-> `並不能保證，只能保證Transaction被執行並不會違反資料庫上的資料規則，不一定保證著指定任務的結果都會如同開發者所要達成的目標`
<!--SR:!2024-06-30,360,250-->


#🧠 DB: 每一個Transaction都一定有consistency這特性嗎？ ->->-> `Consistency 不一定就實現在每個協議，具體還要看資料庫系統是否支援和開發者是否添加特定語法`
<!--SR:!2024-08-29,483,250-->


#🧠 Consistency 是指只要執行協議上的指定任務之後都能產生同個結果，其結果為其資料庫上的資料都會是維持著合法的特性，其中合法是指什麼？ ->->-> `合法是指滿足資料庫對於資料上的規則`
<!--SR:!2023-11-29,90,230-->


---
Status: #🌱 
Tags:
[[Database]] - [[Transaction]]
Links:
[[Transaction - Atomicity 是指協議上所有被執行的任務直接都視為一個不可分割的原子，任何一個任務不能單獨被完成，只有全部任務完成或者全部任務不完成]]
[[Database transaction 是指資料庫要替特定對象A提供特定資料的存取所要滿足的協議，其協議內容為一些資料庫系統所要執行的代碼和附加執行規則]]
References:
[[@wikidataACID2022]][[@guojiajiaoyuyanjiuyuanGuoJiaJiaoYuYanJiuYuanShuangYuCiHuiXueShuMingCiJiCiShuZiXunWang]]
[[@cambridgedictionaryConsistencyTranslateTraditional]]