## 描述

### CSS 開發順序

> 概念上，每個區塊都會經歷一個「排版>區塊>內容>動畫」的 loop。採用流水式一區一區往下切的話，容易忽略掉區塊之間的交互關係 (例如螢幕尺寸調整時，區塊位置需要互換)，而陷入牽一髮動全身的窘境中，需要再回頭改掉已經做好的細節。


![](https://assets-lighthouse.alphacamp.co/uploads/image/file/16202/ExportedContentImage_02.png)


### css樣式屬性擺放方式

> 學了 CSS 學習架構以後，我們可以運用其「由外而內」的脈絡，將屬性按照「排版>區塊>內容>動畫」的順序一一擺入，並適當加入一些註解：


```
/*good example*/
/* Basic comment */
.target-classname,
.other-target {
    /* Positioning */
    position: relative;
    top: 100px;
    left: 100px;
    
    /* Display */
    display: flex;
    justify-content: center;
    
    /* Box Model */
    width: 100px;
    height: 20px;
    border-radius: 3px solid #ccc;
    
    /* Font or other */
    font-size: 18px;
    line-height: 20px;
    color: #333;
    background: #fff;
}

```

### CSS 命名建議

> CSS 的 class 與 id 命名上，如果團隊沒有特殊規定，一般的通則是建議使用 [Kebab-case](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841)，也就是像烤肉串一樣用 `-` 來連接每個單字，而 Camel Case (駝峰式) 則留給 JavaScript 變數命名：

```
/* Camel Case，不建議 */
.targetClassName {
  ...
}
/* Kebab Case，建議 */
.target-class-name {
  ...
}
```

### 斷行與空格

> 當多個選擇器套用相同樣式時，建議要讓每個選擇器逗號後面斷行，另外「選擇器與括號」之間和「屬性名後面的冒號與值」之間都要保留一個空白，增加易讀性：

```
 /* Bad */
    .class-one, .class-two, .class-three{ 
        position:relative;
    }
/* Good */
    .class-one,
    .class-two,
    .class-three { 
        position: relative; 
    }
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[CSS]]
Links:
References: