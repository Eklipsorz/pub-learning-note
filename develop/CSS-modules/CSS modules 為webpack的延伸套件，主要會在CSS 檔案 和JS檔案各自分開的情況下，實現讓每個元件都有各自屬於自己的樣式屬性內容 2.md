
## 描述
> The separation of CSS and JavaScript

> css module
>
> - is a feature which is only available in projects that are configured to support it because it needs a code transformation that needs to be done before your code runs in the browser
>
> - now the good thing is react projects created with create react app which we used are already configured to support CSS Modules


### 主要用途為
在CSS 檔案 和JS檔案各自分開的情況下，實現讓每個元件都有各自屬於自己的樣式屬性內容


### CSS Modules 具體是webpack 延伸套件
- 具體會是 webpack 延伸套件
	- 若要使用的話，得確保webpack是否支援該套件以及相關設定檔案
	- 預設下，React的CRA有支援CSS modules 和 其設定
- 由於是由webpack負責將特定CSS轉換成CSS Module來處理和轉換，所以得要把要處理的CSS檔案名稱，改成以下形式：origin-file-name為原本檔案名，後面的module.css則是後綴字
```
<origin-file-name>.module.css
```
- 舉例：
	- test.module.css

### 使用方式
1. 載入特定 module.css 並以其CSS內容作為物件來存取，並且讓styles參照該物件
```
import styles from <css-file>
```

2. 依據著對應內容上的class-selector來選擇想要使用的樣式名稱，每個class-selector會是styles物件下的屬性。
```
<button className={styles.button} />
```


#### 物件名稱選擇
```
import styles from <css-file>
import classes from <css-file>
```


actually for code transformation, which behind the scenes to happen, you also need to rename your file a little bit

  
#### 總結
- 會將對應的css檔案視作為JS下的object
- 每個object的屬性會是該css下的class selector name

  


### 實際轉換

當webpack 將特定CSS以CSS Modules 來處理時，
```
import styles from <css-file>
```

會為CSS檔案內容的所有class selector生成一個獨立且隨機的識別字來重新命名這些class selector名稱，包括以下形式的class，皆會生成獨立且隨機的識別字來重新命名
```
.class1 {...}
.class1.class2 {...}
.class1 .class2 {...}
// result
.class1 => waer324
.class2 => warewa32

.class1 {...} => .waer324 {...}
.class1.class2 {...} => .waer324.warewa32 {...}
.class1 .class2 {...} => .waer324 .warewa32 {...}
```


接著若元件的樣式是以物件形式來取得裡頭的class selector，實際上對應DOM節點的class屬性值會以class selector的對應識別字，對應識別字名稱形式會是：
```
<component-name>_<class-selector-name>_<unique-hash-value>
```



#### 案例
假若CSS 檔案為如下：
```
.button {
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
}

.button:focus {
  outline: none;
}

.button:hover,
.button:active {
  background: #ac0e77;
  border-color: #ac0e77;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}
```

並且在React的層級定義使用button這class selector作為button的外觀設定
```
<button className={styles.button} />
```


經由webpack和CSS modules的轉換後的CSS內容為：
```
.Button_button_wae1232wer {
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
}

.Button_button_wae1232wer:focus {
  outline: none;
}

.Button_button_wae1232wer:hover,
.Button_button_wae1232wer:active {
  background: #ac0e77;
  border-color: #ac0e77;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}
```

而對應button的實際DOM節點會是
```
<button class="Button_button_wae1232wer"></button>
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]] - [[CSS]]
Links:
References:

