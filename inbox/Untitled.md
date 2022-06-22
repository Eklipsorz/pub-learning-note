## 描述
[[@piotrkononowReasonsWhyThere]] 所描述：
> ## Why is that a problem?

> ### 1. Potential data integrity issues, duh
> The obvious problem with the lack of foreign keys is that a database can't enforce referential integrity and if it wasn't taken care of properly at the higher level then this might lead to inconsistent data (child rows without corresponding parent rows).

> ### 2. Tables relations are not clear
> Another, less visible, negative effect of lack of foreign keys in a database is that people who don't know the schema have a hard time finding the right tables and figuring out table relations. This may lead to [serious problems](https://dataedo.com/blog/2-common-sql-join-traps-with-test-queries) with querying and reporting from the database.


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@piotrkononowReasonsWhyThere]]
[[@postgresdexiaodaogushiYiZiLiaoKuZhongBuShiYongWaiBuJianDeGeLiYou]]