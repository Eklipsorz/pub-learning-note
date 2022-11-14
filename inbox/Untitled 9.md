

## 描述

### 歷經event flow的多個元件的執行順序
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


重點：
- 從結果來看
## 複習


---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
References: