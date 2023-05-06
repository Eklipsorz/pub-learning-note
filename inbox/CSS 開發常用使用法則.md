## 描述

### CSS 開發順序

> 概念上，每個區塊都會經歷一個「排版>區塊>內容>動畫」的 loop。採用流水式一區一區往下切的話，容易忽略掉區塊之間的交互關係 (例如螢幕尺寸調整時，區塊位置需要互換)，而陷入牽一髮動全身的窘境中，需要再回頭改掉已經做好的細節。


![](https://assets-lighthouse.alphacamp.co/uploads/image/file/16202/ExportedContentImage_02.png)

重點：
- 開發順序是基於架構式，將架構中的每個區塊位置排好，然後再調整每個區塊的細節
- 若採用以一區為一個單位來完成排版和樣式，會忽略區塊之間的位置相互關係，而陷入必須要不斷花時間修正的問題


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

重點：
- 註解可以依照排版、區塊、內容、動畫來增加註解
- 排版、區塊的註解會是 
```
    /* Positioning */
    position: relative;
    top: 100px;
    left: 100px;
    
    /* Display */
    display: flex;
    justify-content: center;
```
- 內容註解為
```
    /* Box Model */
    width: 100px;
    height: 20px;
    border-radius: 3px solid #ccc;
    
    /* Font or other */
    font-size: 18px;
    line-height: 20px;
    color: #333;
    background: #fff;
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

重點：
- 使用Kebab-case 來命名每個selector名稱，Camel Case留給駝峰式

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

重點：
- 若有多個選擇器套用相同樣式，形式最好是每個選擇器逗號後面斷行
- 選擇器和括號之間要留空白
- 屬性名稱和屬性值之間要留空白

## 複習
#🧠 當要開發網頁前端時，前期要如何安排每個開發區塊會比較好？ ->->-> `是基於架構式，將架構中的每個區塊位置排好，然後再調整每個區塊的細節`
<!--SR:!2023-06-09,34,246-->



#🧠 當用HTML和CSS來開發網頁前端時，先完成一個元件的呈現內容接著爾後完成每個元件的排版位置，這樣會有甚麼問題？->->-> `會忽略區塊之間的位置相互關係，而陷入必須要不斷花時間修正的問題`
<!--SR:!2023-05-22,42,210-->

#🧠 CSS開發區塊大致上可以區分哪四種？ ->->-> `註解可以依照排版、區塊、內容、動畫來增加註解`
<!--SR:!2023-05-27,93,230-->


#🧠 CSS註解會如何表明結構？請用註解來表示 ->->-> `排版、區塊是 /* position */ /* display */，而內容註解則是 /* Box Model */ /* Font or other */`
<!--SR:!2023-06-28,70,230-->


#🧠 CSS selector 名稱的命名方式如何？ ->->-> `Kebab-case`
<!--SR:!2023-07-05,71,230-->


#🧠  CSS：當多個選擇器套用相同樣式時，怎麼樣的寫法會比較易讀？ ->->-> `若有多個選擇器套用相同樣式，形式最好是每個選擇器逗號後面斷行`
<!--SR:!2023-05-21,155,250-->

#🧠 在普遍的CSS開發上，CSS Selector 名稱和括號保持什麼？->->-> `選擇器和括號之間要留空白`
<!--SR:!2023-05-20,155,250-->

#🧠 在普遍的CSS開發上，屬性名稱會和屬性值保持什麼？ ->->-> `屬性名稱和屬性值之間要留空白`
<!--SR:!2023-07-20,194,250-->


---
Status: #🌱 
Tags:
[[CSS]]
Links:
References: