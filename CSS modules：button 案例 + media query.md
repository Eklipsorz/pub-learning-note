## 描述


### css 原檔 經過 CSS modules 後會重新命名

命名前：
```
.button {
  width: 100%;
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

@media (min-width: 768px) {
  .button {
    width: auto;
  }
}
```

命名後：將重命名的
```
.Button_button__2lgkF {
  width: 100%;
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
}

.Button_button__2lgkF:focus {
  outline: none;
}

.Button_button__2lgkF:hover,
.Button_button__2lgkF:active {
  background: #ac0e77;
  border-color: #ac0e77;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}

@media (min-width: 768px) {
  .Button_button__2lgkF {
    width: auto;
  }
}
```

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]] - [[CSS]]
Links:
[[CSS modules 為webpack的延伸套件，主要會在CSS 檔案 和JS檔案各自分開的情況下，實現讓每個元件都有各自屬於自己的樣式屬性內容]]
References: