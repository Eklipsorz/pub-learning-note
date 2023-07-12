
  

## REST 等級模型

1. 目的在於：以REST約束來評估一個Web服務設計的好壞並做個分級

2. 等級模型起草於Leonard Richardson在2008年 QCon Talk中，並於2010年由Martin Fowler進一步詮釋模型，並使該模型更加完整

3. 等級大致上分為：

- Level 0：將整個Web服務規劃成一個URI，並只用一個HTTP動詞來進行客戶端和伺服器之間的互動方式，通常HTTP動詞會是POST

- Level 1：將整個Web服務依據資源來分成多個URI，但只用一個HTTP動詞來進行客戶端和伺服器之間的互動方式

- Level 2：將整個Web服務依據資源來分成多個URI，並分成多個HTTP動詞來進行客戶端和伺服器之間的互動方式

- Level 3：基於Level2的概念下使用HATEOAS概念。

![](https://devopedia.org/images/article/252/1821.1579540894.jpg)

參考資料：

[你的REST不是REST？](https://www.ithome.com.tw/voice/128528)

[Richardson Maturity Model](https://devopedia.org/richardson-maturity-model)

