

## 描述

在event flow中，每個接收到事件信號的DOM節點會做什麼
	- 接收事件信號->執行對應事件處理->處理完並轉遞信號

### bubbling phase：歷經event flow的多個元件的執行順序
```
        <div class="grandpa" id="element1">
            <div class="parent" id="element2">
                <div class="child" id="element3">child</div>
            </div>
        </div>
```


```
const element1 = document.querySelector('.grandpa');
const element2 = document.querySelector('.parent');
const element3 = document.querySelector('.child');

function handler() {
  for (let i = 0; i < 1000000000; i++) {}
  console.log('handler', this);
}

element1.addEventListener('click', handler);
element2.addEventListener('click', handler);
element3.addEventListener('click', handler);
```

結果為
```
(隔了 1s 之後出現)
handler <div id="element3" class="child">
(隔了 1s 之後出現)
handler <div id="element2" class="parent">
(隔了 1s 之後出現)
handler <div id="element1" class="grandpa">
```


### capture phase：歷經event flow的多個元件的執行順序

```
        <div class="grandpa" id="element1">
            <div class="parent" id="element2">
                <div class="child" id="element3">child</div>
            </div>
        </div>
```


```
const element1 = document.querySelector('.grandpa');
const element2 = document.querySelector('.parent');
const element3 = document.querySelector('.child');

function handler() {
  for (let i = 0; i < 1000000000; i++) {}
  console.log('handler', this);
}

element1.addEventListener('click', handler, true);
element2.addEventListener('click', handler, true);
element3.addEventListener('click', handler, true);
```

結果為
```
(隔了 1s 之後出現)
handler <div id="element1" class="grandpa">
(隔了 1s 之後出現)
handler <div id="element2" class="parent">
(隔了 1s 之後出現)
handler <div id="element3" class="child">
```



重點：
- 從結果來看，當若是採用bubbling 來接收事件信號時，其接收順序會是從內至外，每個都會接收到的節點都會處理完，才會發送信號
	- element3 一接收信號就執行自己的事件處理，執行完再發送信號至parent element的element2
	- element2 一接收到信號就執行自己的事件處理，執行完再發送信號至parent element的element1
	- element1 一接收到信號就執行自己的事件處理，執行完再發送信號
```
element3 -> element2 -> element1
```
- 若是採用capture phase的話，其接收順序會是從外至內，每個都會接收到的節點都會處理完，才會發送信號
	- element1 一接收信號就執行自己的事件處理，執行完再發送信號至element2
	- element2 一接收到信號就執行自己的事件處理，執行完再發送信號至element3
	- element3 一接收到信號就執行自己的事件處理，執行完再發送信號
```
element1 -> element2 -> element3
```
## 複習

#🧠 在event flow中，若傳遞順序為element1->element2->element3 ，那麼他們是如何處理接收和信號處理，先發送至element1，接著呢？->->-> `element1接收到信號，element1就先處理對應事件處理，然後再發送信號轉遞給element2，element2接收到信號並處理對應事件處理，然後再發送信號轉遞給element3，然後element3接收到信號，並處理對應事件處理，接著發送信號`
<!--SR:!2023-11-06,83,230-->

#🧠 在event flow中，每個接收到事件信號的DOM節點會做什麼->->-> `接收事件信號->執行對應事件處理->處理完並轉遞信號`
<!--SR:!2023-09-21,193,250-->

#🧠 程式碼如下，假設對element3按下點擊，請問其事件處理的順序和接收順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668439773/blog/javascript/event/event-flow/bubbling-phase-execution-order_zzygfc.png))->->-> `(隔了 1s 之後出現) handler <div id="element3" class="child"> (隔了 1s 之後出現) handler <div id="element2" class="parent"> (隔了 1s 之後出現) handler <div id="element1" class="grandpa">`
<!--SR:!2023-10-17,209,250-->

#🧠 程式碼如下，假設對element3按下點擊，請問其事件處理的順序和接收順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668439773/blog/javascript/event/event-flow/capture-phase-execution-order_dwacbc.png) ->->-> `(隔了 1s 之後出現) handler <div id="element1" class="grandpa"> (隔了 1s 之後出現) handler <div id="element2" class="parent"> (隔了 1s 之後出現) handler <div id="element3" class="child">`
<!--SR:!2024-11-16,443,250-->

#🧠 程式碼如下，假設對element3按下點擊，其事件處理的順序和接收順序是element3 -> element2 -> element1，具體會是，又是什麼phase？？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668439773/blog/javascript/event/event-flow/bubbling-phase-execution-order_zzygfc.png) ->->-> `由於是採用bubbling phase來接收，所以就是： element3 一接收信號就執行自己的事件處理，執行完再發送信號至parent element的element2 - element2 一接收到信號就執行自己的事件處理，執行完再發送信號至parent element的element1 - element1 一接收到信號就執行自己的事件處理，執行完再發送信號`
<!--SR:!2023-09-22,194,250-->

#🧠 程式碼如下，假設對element3按下點擊，其事件處理的順序和接收順序是element1 -> element2 -> element3，具體是什麼，又是什麼phase？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1668439773/blog/javascript/event/event-flow/capture-phase-execution-order_dwacbc.png)->->-> `由於是採用capture phase，所以就是	- element1 一接收信號就執行自己的事件處理，執行完再發送信號至element2 - element2 一接收到信號就執行自己的事件處理，執行完再發送信號至element3 - element3 一接收到信號就執行自己的事件處理，執行完再發送信號`
<!--SR:!2023-10-05,198,250-->




---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
References: