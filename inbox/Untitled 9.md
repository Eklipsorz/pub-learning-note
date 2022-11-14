

## 描述

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
element3 -> element2 -> elment1
```
- 若是採用capture phase的話，其接收順序會是從外至內，每個都會接收到的節點都會處理完，才會發送信號
	- element1 一接收信號就執行自己的事件處理，執行完再發送信號至parent element的element2
	- element2 一接收到信號就執行自己的事件處理，執行完再發送信號至parent element的element3
	- element3 一接收到信號就執行自己的事件處理，執行完再發送信號
```
element1 -> element2 -> elment3
```
## 複習


---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
References: