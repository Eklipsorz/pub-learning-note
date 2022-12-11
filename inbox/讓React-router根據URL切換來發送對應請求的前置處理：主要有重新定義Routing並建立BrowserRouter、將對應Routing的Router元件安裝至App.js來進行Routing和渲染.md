## 描述

讓React-router根據URL切換來發送對應請求的前置處理：自製擁有loader功能的BrowserRouter、將Router安裝至RouterProvider元件、


### 讓React-router根據URL切換來發送對應請求的前置處理



#### 問題&解法： loader 和 useLoaderData 技術不被預設的BrowserRouter所支援

loader 和 useLoaderData 技術不被預設的BrowserRouter所支援，換言之，無法讓Router根據URL切換來發送請求

解法是：
- 重新定義Routing並建立BrowserRouter，其中Routing中的每個Route都會有對應Loader來告知React哪些是要以Loader來執行。

步驟：
- [[自製擁有loader功能的BrowserRouter，根據Routing作法：單純使用JS語言體系的物件語法來表示Routing中的每個Route、使用JSX語言體系的元件語法來表示Routing中的每個Route]]
- 將對應Routing的Router元件安裝至App.js來進行Routing和渲染：
	- 將Router物件安裝至RouterProvider元件，使Router物件能夠正常在對應元件進行Routing和渲染
	- 對應RouterProvider安裝至App.js








  


## 複習


---
Status:  #🌱 
Tags:
[[React]]
Links:
[[useLoaderData是react-router v6.4 所提供的hook，其概念為會從元件所待的目前Route元件獲取loader屬性並以promise形式執行對應loader，等到該 loader 執行完畢後才會回傳資料]]
[[react-router-dom v6：RouteProvider 元件用途為Provider形式來管理對應Routing並設定誰能夠使用對應Routing進行渲染]]
[[自製擁有loader功能的BrowserRouter，根據Routing作法：單純使用JS語言體系的物件語法來表示Routing中的每個Route、使用JSX語言體系的元件語法來表示Routing中的每個Route]]

References:
[[@RouterProviderV6]]

