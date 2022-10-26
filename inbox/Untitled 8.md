## 描述

### 補充知識：Render && Rendering



#### 原意

[[@profilephotoforandreiandrosoffWhatDoesRendering]]

> Rendering is the creation of a visual representation - a picture or a movie - of data, such as a 3D model or a video composition.

visual 
> relating to seeing

重點：
- render 是指建立一個視覺上能夠呈現的事物，事物會是圖片、影片
- rendering 是指建立視覺上能夠呈現的事物之過程、方式

### 在網頁上的Render && Rendering 

**建立一個視覺上能夠呈現的事物**，在這裡的事物會是指代表畫面的事物或者畫面本身。

#### Server-Side Rendering 
由伺服器負責建立一組能夠在客戶端以視覺上呈現的事物：
	- 該事物會是代表著特定畫面
	- 事物會是由一組由CSS、JS、HTML檔案所構成，可直接由客戶端瀏覽器解析呈現，不需要額外程式進行


#### Client-Side Rendering 
由客戶端負責建立一組能夠在自身平台以視覺上呈現的事物：
	- 該事物會是代表著特定畫面
	- 事物會是由對應Virtual DOM或者Real DOM來表示，通常會由



- 以Client-Server來說：根據請求的不同來通過程式碼邏輯來生成對應的View，而SSR和CSR所產生的View分別為HTML形式或者對應新的DOM結構。

- 單從瀏覽器來說：解析DOM後並對瀏覽器上的pixel進行paint

  

3. website rendering：則是指網頁本身的轉換行為，可根據伺服器或者客戶端而有所不同：

- Server Rendering：將模板檔案搭配資料來生成客戶端可直接呈現的檔案形式，通常為HTML、CSS、JS

- Client Rendering：將HTML、CSS、JS以視覺形式來呈現在客戶端上。


## 複習


---
Status: #🌱 
Tags:
Links:
References:
[[@FengSiXin80TiaoXiaoXib]]
[[@profilephotoforandreiandrosoffWhatDoesRendering]]