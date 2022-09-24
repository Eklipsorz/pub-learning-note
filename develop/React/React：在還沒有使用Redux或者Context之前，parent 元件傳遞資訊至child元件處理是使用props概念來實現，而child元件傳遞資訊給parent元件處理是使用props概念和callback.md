## 描述


### props 傳遞是不可跨越
props傳遞是運用parent 元件的資訊來傳遞至該元件下的child元件，那麼假使元件是三個元件：元件A、元件B、元件C，其中元件A包含元件B，而元件B包含元件C，在這裏，要從元件A傳遞資訊至元件C，必須得經由元件B並委託元件B幫忙傳遞至元件C，也就是
```
A->B->C
```

無法直接這樣傳遞
```
A->C
```


### communication: parent to child 
目標為：
1. 讓child元件存取到parent元件所給予的資訊，並於child元件內處理資訊

實現方式為：
- 藉由props概念來去實現：
	1. parent 元件將自己所擁有的資訊藉由props概念往下傳遞至child元件
	2. child元件使用自己的props來接收其資訊並做處理

### communication: child to parent
目標為
1. 讓parent元件存取到child元件所給予的資訊，並於parent元件內進行處理

實現方式為
- 藉由props概念＋callback來實現：
	- 具體在parent元件上建立callback**來叫child元件去做parent接收到資料時會做的事情**，並以props給予child元件
	- child元件呼叫callback即可，就會去做parent接收到資料時會做的事情。


## 複習
#🧠 React ： 假使元件是三個元件，元件A、元件B、元件C，其中元件A包含元件B，而元件B包含元件C，那麼元件A要如何傳遞資訊至元件C? ->->-> `在這裏，要從元件A傳遞資訊至元件C，必須得經由元件B並委託元件B幫忙傳遞至元件C，也就是A->B->C`
<!--SR:!2022-10-03,27,250-->

#🧠 React ： 假使元件是三個元件，元件A、元件B、元件C，其中元件A包含元件B，而元件B包含元件C，那麼元件A要如何傳遞資訊至元件C? A能夠直接傳遞到C嗎 ->->-> `不能`
<!--SR:!2022-11-16,53,250-->

#🧠 React： 為了讓child元件存取到parent元件所給予的資訊，並於child元件內處理資訊，請問實現方式為何？ ->->-> `- 藉由props概念來去實現： 1. parent 元件將自己所擁有的資訊藉由props概念往下傳遞至child元件 2. child元件使用自己的props來接收其資訊並做處理`
<!--SR:!2022-10-16,28,230-->

#🧠 React： 為了讓parent元件存取到child元件所給予的資訊，並於parent元件內處理資訊，請問實現方式為何？ ->->-> `- 藉由props概念＋callback來實現： - 具體在parent元件上建立callback**來叫child元件去做parent接收到資料時會做的事情**，並以props給予child元件 - child元件呼叫callback即可，就會去做parent接收到資料時會做的事情。`
<!--SR:!2022-09-26,22,250-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: