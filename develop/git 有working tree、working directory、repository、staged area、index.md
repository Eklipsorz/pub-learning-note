
## 描述

git 系統當中，有五個主要的空間名詞，
> The working tree is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

- working directory & working tree：
	- 兩者都是以目錄來存放特定版本下的檔案內容
	- 之所以會用tree來描述，也是強調著目錄會是以tree來構成
	- 可參考於[[working tree 是指特定版下的物件轉換成儲存空間的檔案和目錄，並由樹狀或目錄管理]]

- staging area & index：
	- 兩者都是一樣的，皆指為專門儲存哪些內容是 **準備提交至下一個版本的內容**。
	- 其中，index是Git 實現上的專業術語
	- 以檔案形式來紀錄哪些檔案內容A會是下一個版本的內容
	- 可參考於 [[staging area 和 index 兩者皆為一樣]]

- repository：
	- 用途為會存放不同時期下的版本內容或者提交內容
	- 會是以.git隱藏目錄來儲存git對於本地端repo的設定以及一組資料庫來儲存不同時期下的版本內容。
	- 可參考於 [[@scottchaconGitWhatGit]]

## 流程
在這裡會是以某個版本的內容來作為working directory，staging area則是準備提交至repo資料庫的站存區，.git directory則是代表著repository。
![](https://git-scm.com/book/en/v2/images/areas.png)

流程：
- 當特定版本的內容有出現變動時，也就是Working Directory包含的內容有變動的話
- 下達git add 指定哪些內容成為下一個版本的內容，這時會是從working directory至staging area
- 接著再下達git commit來提交目前暫存的內容至下一個版本，具體會存進repository，也就是從staging area傳至repository


### note
1. 若於一開始下達git init來建立git系統的話，請問working directory 會是什麼？
預設上會是無內容的目錄來代表目前所處於的版本。
## 複習
#🧠 working directory & working tree  是什麼？ 用途是什麼？ ->->-> `以目錄來存放特定版本下的檔案內容，之所以會用tree來描述，也是強調著目錄會是以tree來構成`
<!--SR:!2022-07-04,25,248-->

#🧠 staging area & index 是什麼？用途是什麼？ ->->-> `兩者都是一樣的，皆檔案形式來專門儲存哪些內容是 **準備提交至下一個版本的內容**。`
<!--SR:!2022-07-06,28,250-->

#🧠 repository是什麼？用途是什麼？ ->->-> `會是以.git隱藏目錄來儲存git對於本地端repo的設定以及一組資料庫來儲存不同時期下的版本內容，用途為會存放不同時期下的版本內容或者提交內容`
<!--SR:!2022-07-23,36,230-->

#🧠  若於一開始下達git init來建立git系統的話，請問working directory 會是什麼 ->->-> `預設上會是無內容的目錄來代表目前所處於的版本`
<!--SR:!2022-07-12,31,248-->

#🧠 請描述Working Directory、Staging Area、.git directory(Repository)會是指什麼 ![](https://git-scm.com/book/en/v2/images/areas.png) ->->-> `在這裡會是以某個版本的內容來作為working directory，staging area則是準備提交至repo資料庫的站存區，.git directory則是代表著repository`
<!--SR:!2022-06-21,17,250-->

#🧠 請描述這些流程如何運作？ ![](https://git-scm.com/book/en/v2/images/areas.png) ->->-> `1. 當特定版本的內容有出現變動時，也就是Working Directory包含的內容有變動的話。2. 下達git add 指定哪些內容成為下一個版本的內容，這時會是從working directory至staging area，3. 接著再下達git commit來提交目前暫存的內容至下一個版本，具體會存進repository，也就是從staging area傳至repository` 
<!--SR:!2022-07-18,34,248-->

---
Status: #🌱 
Tags:
[[Git]]
Links:
[[working tree 是指特定版下的物件轉換成儲存空間的檔案和目錄，並由樹狀或目錄管理]]
[[staging area 和 index 兩者皆為一樣]]
References:
 [[@scottchaconGitWhatGit]]