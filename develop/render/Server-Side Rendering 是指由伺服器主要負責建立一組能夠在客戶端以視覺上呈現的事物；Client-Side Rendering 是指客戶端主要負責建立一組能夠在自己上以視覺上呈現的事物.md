## 描述

### 補充知識：Render && Rendering



#### 在電腦科學中

[[@profilephotoforandreiandrosoffWhatDoesRendering]]

> Rendering is the creation of a visual representation - a picture or a movie - of data, such as a 3D model or a video composition.

visual 
> relating to seeing

重點：
- render 是專指建立一個視覺上能夠呈現的事物，事物會是圖片、影片
- rendering 是指建立視覺上能夠呈現的事物之過程、方式

### 在網頁上的Render && Rendering 

**建立一個視覺上能夠呈現的事物**，在這裡的事物會是指代表畫面的事物或者畫面本身。

#### Server-Side Rendering 
由伺服器主要負責建立一組能夠在客戶端以視覺上呈現的事物：
	- 該事物會是代表著特定畫面的特定事物
	- 事物會是由一組由CSS、JS、HTML檔案所構成，可直接由客戶端瀏覽器解析呈現，不需要額外程式進行


#### Client-Side Rendering 
由客戶端主要負責建立一組能夠在自身平台以視覺上呈現的事物：
	- 該事物會是代表著特定畫面的特定事物
	- 事物會是由對應Virtual DOM或者Real DOM來表示，若事物會是Virtual DOM的話，會需要額外程式轉換成Real DOM來呈現


#### 瀏覽器

單從瀏覽器來說：瀏覽器建立一組能夠在瀏覽器呈現的事物，具體會是指：
	- 事物會是指畫面本身
	-  將DOM 和CSSOM合併成Rendering Tree後、並計算位置、針對瀏覽器上的pixel進行paint


## 複習

#🧠 render 在電腦科學中是什麼意思？ ->->-> `render 是指建立一個視覺上能夠呈現的事物`
<!--SR:!2024-12-04,469,250-->

#🧠 render 在電腦科學中是指建立一個視覺上能夠呈現的事物，其中事物會是什麼？ ->->-> `圖片、影片`
<!--SR:!2023-12-10,89,210-->

#🧠 rendering 在電腦科學中是什麼意思？ ->->-> `建立視覺上能夠呈現的事物之過程、方式`
<!--SR:!2024-11-21,460,250-->


#🧠 在網頁上的Render && Rendering，**建立一個視覺上能夠呈現的事物**，在這裡的事物會是什麼 ->->-> `代表畫面的事物或者畫面本身。`
<!--SR:!2024-07-24,375,250-->

#🧠 Render && Rendering 在 Server-Side Rendering 會是什麼意思？其事物會是什麼？  代表畫面的事物？代表畫面本身？->->-> `由伺服器主要負責建立一組能夠在客戶端以視覺上呈現的事物，事物會該事物會是代表著特定畫面的特定事物，主要是由一組由CSS、JS、HTML檔案所構成，可直接由客戶端瀏覽器解析呈現，不需要額外程式進行`
<!--SR:!2024-05-04,290,230-->


#🧠 Server-Side Rendering 是由伺服器主要負責建立一組能夠在客戶端以視覺上呈現的事物，其中事物是 代表畫面的事物？代表畫面本身？具體說明->->-> `	- 該事物會是代表著特定畫面的特定事物 - 事物會是由一組由CSS、JS、HTML檔案所構成，可直接由客戶端瀏覽器解析呈現，不需要額外程式進行`
<!--SR:!2024-03-17,307,250-->



#🧠 Client-Side Rendering 是由客戶端主要負責建立一組能夠在自身平台以視覺上呈現的事物，其中事物是 代表畫面的事物？代表畫面本身？具體說明->->-> `	- 該事物會是代表著特定畫面的特定事物 - 事物會是由對應Virtual DOM或者Real DOM來表示，若事物會是Virtual DOM的話，會需要額外程式轉換成Real DOM來呈現`
<!--SR:!2023-10-13,210,250-->

#🧠  Render && Rendering 在 Client-Side Rendering 會是什麼意思？其事物會是什麼？ 代表畫面的事物？代表畫面本身？具體說明->->-> `由客戶端主要負責建立一組能夠在自身平台以視覺上呈現的事物，該事物會是代表著特定畫面的特定事物，事物會是由對應Virtual DOM或者Real DOM來表示，若事物會是Virtual DOM的話，會需要額外程式轉換成Real DOM來呈現`
<!--SR:!2024-09-03,407,250-->


#🧠 在代表畫面的事物和代表畫面本身來說，Server-Side Rendering 、 Client-Side Rendering、瀏覽器本身產出的視覺上呈現的事物，會是什麼？->->-> `前兩者是代表畫面的事物、最後一個則是畫面本身`
<!--SR:!2024-08-25,404,250-->

#🧠 Render && Rendering 在瀏覽器本身會是什麼？ 代表畫面的事物？代表畫面本身？ ->->-> `瀏覽器建立一組能夠在瀏覽器呈現的事物。	- 事物會是指畫面本身 -  將DOM 和CSSOM合併成Rendering Tree後、並計算位置、針對瀏覽器上的pixel進行paint`
<!--SR:!2023-12-01,141,170-->

---
Status: #🌱 
Tags:
[[Rendering]] - [[Client-Side Rendering]] - [[Server-Side Rendering]]
Links:
References:
[[@FengSiXin80TiaoXiaoXib]]
[[@profilephotoforandreiandrosoffWhatDoesRendering]]