## 描述



### template processor
[[@wikidataTemplateProcessor2022]] 所描述
> A template processor (also known as a template engine or template parser) is software designed to combine templates with a data model to produce result documents.
> 
> The language that the templates are written in is known as a template language or templating language.

[[@nikicPhpWhatTemplating]]
> A templating language basically is a language which allows defining placeholders that should later on be replaced for the purpose of implementing designs.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/TempEngGen015.svg/440px-TempEngGen015.svg.png)

重點：
- template processor 技術目的是要將網頁切分成MVC(Model、View、Controller)來開發/維護
- template processor 會提供自己的語言體系語法以及HTML、CSS、JS來建立可填入資料的模板
	- template language 是模板引擎用來製作模板的語言，語言是模板引擎提供且能夠識別並處理
- template processor 會將模板和要放進模板填入的資料合併成一組HTML、CSS、JS組成的網頁

### template language 好處
[[@wikidataTemplateProcessor2022]] 所描述
> encourages organization of source code into operationally-distinct layers (see e.g., MVC)

1. 使網頁開發轉換成MVC架構來方便維護/開發資料(含業務邏輯)、畫面、導向請求這三個部分


## 複習
#🧠 template processor 技術目的是什麼？ ->->-> `網頁切分成MVC(Model、View、Controller)來開發/維護`

#🧠 template language 是什麼？ ->->-> `是模板引擎用來製作模板的語言，語言是模板引擎提供且能夠識別並處理`



#🧠 template processor 會用什麼來建立模板？ ->->-> ` template processor 會提供自己的語言體系語法以及HTML、CSS、JS來建立可填入資料的模板`

#🧠 template processor 會生成什麼結果？過程是？ ->->-> `template processor 會將模板和要放進模板填入的資料合併成一組HTML、CSS、JS組成的網頁`

---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@wikidataTemplateProcessor2022]]
[[@nikicPhpWhatTemplating]]