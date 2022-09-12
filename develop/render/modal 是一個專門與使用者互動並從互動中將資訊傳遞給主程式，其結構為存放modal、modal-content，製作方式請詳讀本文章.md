## 描述

### modal 製作架構為
modal本身是一個元件，高寬皆為viewport的100%，且背景顏色為白色的透明色，元件中間會有個名為dialog-content的對話窗，對話窗內會含有header、body、footer這三個部分，當按下footer的okey或者點dialog任意位置就會讓對話窗消失

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662660001/blog/frontend/dialog/dialog_xeooko.png)

#### 總結
modal：存放整個對話窗和顯示背景為白色的透明色
```
<!-- The Modal -->  
<div id="myModal" class="modal">
	<!-- modal content -->
</div>
```

modal content：對話窗內容
	- header 對話窗上部分，主要放對話窗標題
	- body 對話窗內容，主要放對話窗主要訊息內容
	- footer 對話窗下部分，主要放按鈕
```
<!-- Modal content -->  
<div class="modal-content">  
  <div class="modal-header">  
    <span class="close">&times;</span>  
    <h2>Modal Header</h2>  
  </div>  
  <div class="modal-body">  
    <p>Some text in the Modal Body</p>  
    <p>Some other text...</p>  
  </div>  
  <div class="modal-footer">  
    <h3>Modal Footer</h3>  
  </div>  
</div>
```



### modal 需要的樣式和結構為
1. 一個佔滿viewport的空間：
	- display為fixed + top為0 + left為0  ：確保存放空間是以viewport的起始位置來渲染
	- width為100% + height為100%＋z-index為 99：由於元素為fixed-positioning，其高寬的百分比會受限於viewport，直接設定為100%，就等同於在整個viewport上覆蓋一層

2. 背景色為白色的透明色
	- background-color：rgba(0, 0, 0, 0.8); 設定背景顏色為白色的透明色


```
.modal {
  /* position */
  position: fixed;
  top: 0;
  left: 0;
  z-index: 99;

  /* box model */
  width: 100%;
  height: 100%;

  /* font or other */
  background-color: rgba(0, 0, 0, 0.8);
}
```

3. 能夠存放對話窗整個內容：
```
	// modal
    <div className={styles['modal']} onClick={clickHandler}>
	  // modal-content
      <div className={styles['modal-content']}>
	        ........
      </div>
    </div>
```

### modal content 需要的樣式和結構
1. 將對話窗整個內容擺放中間
	- margin: 10% auto;
2. 設定對話窗的大小
	- width: 30%;

```
.modal-content {
  /* position */
  /* display */
  /* box model */
  margin: 10% auto;
  width: 30%;
  /* font or other */
}
```

3. 定義modal的header、body、footer部分
	- 主要存放header、body、footer這三個部分
```
	<div className={styles['modal-content']}>
        <div className={styles['modal-header']}>
          <h2>{title}</h2>
        </div>
        <div className={styles['modal-body']}>
          <p>{text}</p>
        </div>
        <div className={styles['modal-footer']}>
          <Button onClick={clickHandler}>Okay</Button>
        </div>
    </div>
```

### modal-header 需要的樣式和結構

1. 調整header大小
	- padding: 0.1rem 1rem;
2.  調整header背景顏色
	- background: `#4b0b56`;
3. 設定文字顏色
	- color: `#fff`;
```
.modal-header {
  /* position */
  /* display */
  /* box model */
  padding: 0.1rem 1rem;
  /* font or other */
  color: #fff;
  background: #4b0b56;
}
```

4. 定義header要存的內容
	- 主要存放標題
```
        <div className={styles['modal-header']}>
          <h2>{title}</h2>
        </div>
```

### modal-body 需要的樣式和結構
1. 調整body大小
	- padding: 1rem;
2.  背景顏色按照指定顏色
	- background: `#fff`;

```
.modal-body {
  /* position */
  /* display */
  /* box model */
  padding: 1rem;
  /* font or other */
  background: #fff;
}
```

3. 定義body要存的內容，如訊息
	- 主要存放對話窗的主要資訊內容
```
        <div className={styles['modal-body']}>
          <p>{text}</p>
        </div>
```

### modal-footer 需要的樣式和結構
1. 將按鈕往右邊移動
	- display: flex; + justify-content: flex-end;
2. 調整footer大小
	- padding: 1rem;
3. 調整顏色
	- background: `#fff`;

```
.modal-footer {
  /* position */
  /* display */
  display: flex;
  justify-content: flex-end;
  /* box model */
  padding: 1rem;
  /* font or other */
  background: #fff;
}
```

4. 定義要存放的內容
	- 主要存放按鈕

```
        <div className={styles['modal-footer']}>
          <Button onClick={clickHandler}>Okay</Button>
        </div>
```
### modal 是什麼
[[@ModalWindow2022]]
> In user interface design for computer applications, a modal window is a graphical control element subordinate to an application's main window. 

> A modal window creates a mode that disables the main window but keeps it visible, with the modal window as a child window in front of it. Users must interact with the modal window before they can return to the parent application.


重點：
- 在程式開發中，modal是一個圖形化控制介面，隸屬於parent程式/主程式/由child程式製作，主要用途為代替主程式來與使用者進行互動，並從互動中回傳互動資訊給主程式來處理。
- 常見案例為：
	- 一個顯示錯誤訊息和ok按鈕的小視窗

## 複習

#🧠 在電腦科學的開發中，modal是什麼？ 用途是什麼  ->->-> `modal是一個圖形化控制介面，隸屬於parent程式/主程式/由child程式製作，主要用途為代替主程式來與使用者進行互動，並從互動中回傳互動資訊給主程式來處理`
<!--SR:!2022-09-17,5,249-->

#🧠 在電腦科學的開發中，modal的案例是什麼？ ->->-> `一個顯示錯誤訊息和ok按鈕的小視窗`
<!--SR:!2022-09-13,3,250-->

#🧠 modal 主體架構有什麼？ ->->-> `存放modal本身並顯示白色透明背景顏色的區塊、一個modal主要內容區塊、內容區塊含有header、body、footer，header是modal的上半部、body則是modal所要傳遞的主體、footer則是modal的底部`
<!--SR:!2022-09-13,3,250-->


#🧠 modal 主體架構有什麼？請用下圖來畫出架構 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662724421/blog/frontend/dialog/dialog-origin_tf3iqi.png)->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662660001/blog/frontend/dialog/dialog_xeooko.png)`
<!--SR:!2022-09-13,3,250-->


#🧠 modal主體架構中負責存放modal部分的區塊所要實現的目標是什麼？ ->->-> `一個佔滿viewport的空間、背景為白色的透明色、能夠存放對話窗整個內容`
<!--SR:!2022-09-13,3,250-->


#🧠 modal主體架構中負責存放modal部分的區塊所要實現的目標是一個佔滿viewport的空間、背景色為白色的透明色，請問對應的CSS會是什麼？(請附加註解) ->->-> ` position: fixed;、 top: 0; 、 left: 0;、z-index: 99;、  width: 100%;、height: 100% 、background-color: rgba(0, 0, 0, 0.8);`
<!--SR:!2022-09-13,3,250-->

#🧠 modal主體架構中負責存放modal部分的區塊所要實現的目標是一個佔滿viewport的空間、背景色為白色的透明色，請問對應CSS要求 display為fixed + top為0 + left為0 ，為什麼？->->-> `確保存放空間是以viewport的起始位置來渲染`
<!--SR:!2022-09-13,3,250-->

#🧠 modal主體架構中負責存放modal部分的區塊所要實現的目標是一個佔滿viewport的空間、背景色為白色的透明色，請問對應CSS要求 width為100% + height為100%＋z-index為 99，為什麼？->->-> `由於元素為fixed-positioning，其高寬的百分比會受限於viewport，直接設定為100%，就等同於在整個viewport上覆蓋一層`
<!--SR:!2022-09-13,3,250-->

#🧠 modal主體架構中負責存放modal部分的區塊所要實現的目標是.能夠存放對話窗整個內容，要如何實現？ ->->-> `<div class="modal"> <div class="modal-content"></div> </div>`
<!--SR:!2022-09-16,4,249-->

#🧠 在modal主體架構中，modal-content是負責什麼？->->-> `負責呈現對話視窗本身`
<!--SR:!2022-09-13,2,230-->


#🧠 在modal主體架構中，modal-content的開發目標是什麼？ ->->-> `將對話窗整個內容擺放中間、 設定對話窗的大小、定義modal的header、body、footer部分`
<!--SR:!2022-09-13,3,250-->

#🧠 在modal主體架構中，modal-content的樣式會是什麼？->->-> `  margin: 10% auto; width: 30%;`
<!--SR:!2022-09-16,4,249-->

#🧠 在modal主體架構中，modal-content的html架構會是什麼？ ->->-> ``
<!--SR:!2022-09-17,5,249-->
`

#🧠 在modal主體架構中，modal-header 要實現的目標是什麼？->->-> `調整header大小、調整header背景顏色、設定文字顏色、定義header要存的內容，如標題`
<!--SR:!2022-09-13,3,250-->


#🧠 在modal主體架構中，modal-header 的html結構是什麼 ->->-> `<div> <h2>..</h2> </div>`
<!--SR:!2022-09-13,3,250-->



#🧠 在modal主體架構中，modal-body的開發目標是什麼？->->-> `調整body大小、背景顏色按照指定顏色、定義body要存的內容，如標題`
<!--SR:!2022-09-13,3,250-->


#🧠 在modal主體架構中，modal-body 的html結構是什麼?  ->->-> `        <div className={styles['modal-body']}> <p>{text}</p> </div>`
<!--SR:!2022-09-13,3,250-->

#🧠 在modal主體架構中，modal-footer的開發目標是什麼？ ->->-> `將按鈕往右邊移動、調整footer大小、調整顏色、定義要存放的內容`
<!--SR:!2022-09-13,3,250-->

#🧠 在modal主體架構中，modal-footer 的html結構是什麼? 假使要存按鈕 ->->-> `      <div className={styles['modal-footer']}> <Button onClick={clickHandler}>Okay</Button> </div>`
<!--SR:!2022-09-13,3,250-->



---
Status: #🌱 
Tags:
Links:
[[fixed-positioning 元素的高寬會受限於viewport的高寬 和 absolute-positioning 元素受限於最近的positioned parent 元素的高寬]]
References:
[[@ModalWindow2022]]
