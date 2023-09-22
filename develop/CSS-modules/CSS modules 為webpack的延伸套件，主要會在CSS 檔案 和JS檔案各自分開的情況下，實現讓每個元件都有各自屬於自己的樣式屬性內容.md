
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

  
#### 總結：當webpack 將特定CSS以CSS Modules 來載入處理時，會在開發階段下如何看待和處理
- 會將對應的css檔案視作為JS下的object
- 每個object的屬性會是該css下的class selector name

  


### 實際轉換

當webpack 將特定CSS以CSS Modules 來載入處理且用Button這元件來載入該CSS時，
```
import styles from <css-file>
```

會為CSS檔案內容的所有class selector生成一個獨立且隨機的識別字來重新命名這些class selector名稱，包括以下形式的class，皆會生成獨立且隨機的識別字來重新命名
```
.class1 {...}
.class1.class2 {...}
.class1 .class2 {...}
// result
.class1 => .Button_class1.waer324
.class2 => .Button_class2.warewa32

.class1 {...} => .Button_class1.waer324 {...}
.class1.class2 {...} => .Button_class1.waer324.Button_class2.warewa32 {...}
.class1 .class2 {...} => .Button_class1.waer324 .Button_class2.warewa32 {...}
```


接著若元件的樣式是以物件形式來取得裡頭的class selector，實際上對應DOM節點的class屬性值會以class selector的對應識別字，對應識別字名稱形式會是：
```
<component-name>_<class-selector-name>_<unique-hash-value>
```

#### 轉換條件為
當要對特定CSS檔案進行CSS module的轉換，得滿足：
1. 特定CSS檔案名稱為\<file\>.module.css
2. 要有元件去載入\<file\>.module.css 

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

而對應button的實際DOM節點所獲取到的class會是
```
<button class="Button_button_wae1232wer"></button>
```


## 複習

#🧠 CSS modules  是 CSS-in-JS 的實現嗎？ 為什麼->->-> `並不是，主因為css內容並未納入至js語法的延伸語法，不會根據js的執行狀況來更改css樣式屬性`
<!--SR:!2024-12-20,515,250-->

#🧠 CSS modules 用途是什麼？ 請強調在什麼情況....->->-> `在CSS 檔案 和JS檔案各自分開的情況下，實現讓每個元件都有各自屬於自己的樣式屬性內容`
<!--SR:!2023-11-03,102,230-->

#🧠 CSS modules 在什麼情況下確保每個元件都有各自屬於自己的樣式屬性內容(提示：檔案) ->->-> `在CSS 檔案 和JS檔案各自分開的情況下`
<!--SR:!2023-09-23,221,230-->


#🧠 當要對特定CSS檔案進行CSS module的實際轉換，得滿足什麼條件？ ->->-> `1. 特定CSS檔案名稱為\<file\>.module.css 2. 要有元件去載入\<file\>.module.css `
<!--SR:!2024-01-03,103,208-->

#🧠 CSS modules 具體是什麼套件？ 就說明它源自哪裡->->-> ` 具體會是 webpack 延伸套件`
<!--SR:!2024-11-28,493,250-->

#🧠 CSS modules 具體是 webpack 延伸套件，所以要用的話，那如何做？->->-> `若要使用的話，得確保webpack是否支援該套件以及相關設定檔案`
<!--SR:!2023-10-29,97,230-->

#🧠 CSS modules 由於會將載入的CSS檔案做轉換來給予JS來存取，所以要如何確保webpack不會把一般毫無關係的CSS檔案參與處理？ ->->-> `改成以下形式：origin-file-name為原本檔案名，後面的module.css則是後綴字，並且讓webpack以此作為特別的CSS來處理，就能避免`
<!--SR:!2024-05-05,367,250-->

#🧠 CSS modules 使用方式是如何？ 以一個裝載button樣式的test.module.css和class選擇器為button為例(載入、參考)->->-> `載入特定 module.css 並以其CSS內容作為物件來存取，並且讓styles參照該物件：import styles from <css-file>。依據著對應內容上的class-selector來選擇想要使用的樣式名稱，每個class-selector會是styles物件下的屬性。：<button className={styles.button} />`
<!--SR:!2023-10-21,29,190-->

#🧠 當webpack 將特定CSS以CSS Modules 來載入處理時，會在開發階段下如何看待和處理 ->->-> `- 會將對應的css檔案視作為JS下的object - 每個object的屬性會是該css下的class selector name`
<!--SR:!2024-03-27,271,230-->

#🧠 當webpack 將特定CSS以CSS Modules 來載入處理時，那麼經過webpack處理後的樣式會是如何？(增加命名和載入) ->->-> `會為CSS檔案內容的所有class selector生成一個獨立且隨機的識別字來重新命名這些class selector名稱，包括以下形式的class，皆會生成獨立且隨機的識別字來重新命名，接著若元件的樣式是以物件形式來取得裡頭的class selector，實際上對應DOM節點的class屬性值會以class selector的對應識別字`
<!--SR:!2024-01-05,105,227-->


#🧠 當webpack 將特定CSS以CSS Modules 來載入處理時，那麼經過webpack處理後的樣式名稱會是什麼形式？ ->->-> `<component-name>_<class-selector-name>_<unique-hash-value>`
<!--SR:!2023-10-30,98,230-->

#🧠 假若CSS 檔案內容為如下，並且在React的層級讓Button元件使用該CSS檔案，定義使用button這class selector作為button的外觀設定 \<button className=\{styles.button\} \/\> 經由webpack和CSS modules的轉換後的CSS內容為何？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662292995/blog/react/style/css%20module/CSS-modules-button-example_jdsi6s.png)->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681480906/blog/css/css-module/css-module-result_w0wi6k.png)
<!--SR:!2024-02-02,193,230-->


#🧠 CSS module：假若CSS 檔案內容為如下，並且在React的層級讓Button元件使用該CSS module，定義使用button這class selector作為button的外觀設定 \<button className=\{styles.button\} \/\> 而對應button的實際DOM節點所獲取到的class會是 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662292995/blog/react/style/css%20module/CSS-modules-button-example_jdsi6s.png)->->-> `<button class="Button_button_wae1232wer"></button>`
<!--SR:!2023-10-01,185,210-->


#🧠 當webpack 將特定CSS以CSS Modules 來載入處理時，會替CSS內部和引用方做哪些事情 ->->-> `針對class selector和替換class selector`
<!--SR:!2024-01-09,109,227-->


#🧠 當webpack 將特定CSS以CSS Modules 來載入處理且以Button這元件來載入CSS module時，假如內容有.class1 {...}，請問轉換結果為？ ->->-> `.class1 => .Button_class1_waer324 結果為.class1 {...} => .Button_class1_waer324 {...}`
<!--SR:!2023-11-16,262,247-->


#🧠 當webpack 將特定CSS以CSS Modules 且以Button這元件來載入CSS module時，假如內容有.class1.class2 {...}，請問轉換結果為？->->-> `.class1 => .Button_class1_waer324  .class2 => .Button_class2_warewa32 結果為.class1.class2 {...} => .Button_class1_waer324..Button_class2_warewa32 {...}`
<!--SR:!2024-04-17,268,228-->



#🧠 當webpack 將特定CSS以CSS Modules 且以Button這元件來載入CSS module時，假如內容有.class1 .class2 {...}，請問轉換結果為？->->-> `.class1 => .Button_class1.waer324  .class2 => .Button_class2.warewa32 結果為.class1 .class2 {...} => .Button_class1.waer324 .Button_class2.warewa32 {...}`
<!--SR:!2023-11-05,257,247-->

#🧠 CSS modules 如何防止CSS全域污染問題 ->->-> `主要會讓元件A使用的CSS檔案所擁有的class selector name更名成獨特不重複的，最後再讓元件A使用該CSS檔案下的selector name轉換成更名後的樣子`
<!--SR:!2023-11-27,247,247-->


#🧠 styled-components 和 CSS modules 對於防止CSS全域污染問題的解決概念是什麼？(CSSOM)->->-> `替每個元件正在使用的selector name在同一個CSSOM上是獨特不重複`
<!--SR:!2024-01-02,102,227-->

---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References:

