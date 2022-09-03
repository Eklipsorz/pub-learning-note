
CSS Modules：
- 實現讓每個元件都有各自屬於自己的樣式屬性內容

The separation of CSS and JavaScript


> css module
>
> - is a feature which is only available in projects that are configured to support it because it needs a code transformation that needs to be done before your code runs in the browser
>
> - now the good thing is react projects created with create react app which we used are already configured to support CSS Modules



```
import styles from <css-file>
import classes from <css-file>
```


actually for code transformation, which behind the scenes to happen, you also need to rename your file a little bit

  

- 會將對應的css檔案視作為JS下的object

- 每個object的屬性會是該css下的class selector name

  

  

為了讓webpack能夠識別哪些是CSS module，得讓對應CSS的檔案取名為
```
<origin-file-name>.module.css
```

```
import styles from <css-file>
<button className={styles.button} />
```


當webpack 將特定CSS以CSS Modules 來處理時，會為CSS檔案內容的所有class selector生成一個獨立且隨機的識別字來重新命名這些class selector名稱，同時幫助系統來辨別這些class selector，接著若元件的樣式是採用裡頭的class selector，則是實際上對應DOM節點的class屬性值會以class selector的對應識別字


對應識別字名稱形式會是：
```
<component-name>_<class-selector-name>_<unique-hash-value>
```



案例：
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
