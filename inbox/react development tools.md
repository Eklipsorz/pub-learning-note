## 描述


react development (React 專用的開發除錯工具)

- React Dev tools (會在瀏覽器除錯工具那邊增加Components 和 Profiler)

  

Components tab：(只會以React的角度來觀看網頁)

- component tree (real react component and component structure that is responsible for this UI output.)

- component (props 資訊、hook資訊)

props 資訊

一般：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662310818/blog/react/debug/component-info1_e9ywbc.png)

顯示hooks資訊部分：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662310818/blog/react/debug/component-info2_iinenk.png)

### hooks 資訊
顯示目前元件所綁定的hook function有哪些和目前狀態

### props 資訊


### rendered by 資訊
顯示目前元件由哪個元件負責渲染，會以一份清單來表示，第一個項目會是負責建構目前元件，第二個項目則是負責建構第一個項目，後面依此類推

### source 資訊
顯示目前元件由哪個元件的哪一行負責渲染

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: