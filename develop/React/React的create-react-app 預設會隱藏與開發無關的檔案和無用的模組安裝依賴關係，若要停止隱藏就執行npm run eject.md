## 描述


[[@casieberReactjsWhatDoes]] 所描述
> create-react-app encapsulates all of the npm modules it is using internally, so that your package.json will be very clean and simple without you having to worry about it.

> However, if you want to start doing more complex things and installing modules that may interact with modules create-react-app is using under the hood, those new modules need to know what is available and not, meaning you need to have create-react-app un-abstract them.

> That, in essence, is what `react-scripts eject` does. It will stop hiding what it's got installed under the hood and instead eject those things into your project's package.json for everyone to see.

重點：
- Create-React-App(CRA)
- CRA所建立的開發環境預設會
	- 隱藏與開發無關的檔案
	- 隱藏相關模組安裝依賴關係(如package.json)
- 若要停止隱藏，就執行

```
npm run eject
```

### 潛在的問題

npm run eject
[[@facebookAvailableScriptsCreate]] 提到：
> **Note: this is a one-way operation. Once you `eject`, you can’t go back!**

開發用
> it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc.) into your project as dependencies in `package.json`. Technically, the distinction between dependencies and development dependencies is pretty arbitrary for front-end apps that produce static bundles.

模組依賴問題：
> In addition, it used to cause problems with some hosting platforms that didn't install development dependencies (and thus weren't able to build the project on the server or test it right before deployment). You are free to rearrange your dependencies in `package.json` as you see fit.



重點：
- 一旦執行eject，就無法還原
- 新增加進來模組安裝依賴增加至package.json，有些部署平台無法正常安裝，這會導致無法進行建置或者在部署之前就測試正確
- 新增被隱藏的模組依賴至package.json並不會區分哪些開發的？哪些是原本被隱藏的？


## 複習
#🧠 React： 請問CRA是什麼？ ->->-> `是指react中的create-react-app工具`
<!--SR:!2024-11-24,460,230-->

#🧠 React：請問CRA預設會隱藏什麼？ ->->-> `隱藏與開發無關的檔案、隱藏相關模組安裝依賴關係(如package.json)`
<!--SR:!2023-12-23,110,230-->

#🧠 React：請問若要停止CRA所隱藏的東西，請問要如何做->->-> `npm run eject`
<!--SR:!2024-06-21,410,250-->

#🧠 React：當在CRA所建立的環境下執行npm run eject，會發生什麼 ->->-> `所有原本被隱藏的檔案會直接複製回來、原本隱藏的模組安裝依賴關係會被重寫至package.json`
<!--SR:!2023-06-08,189,250-->

#🧠 React：執行npm run eject後，能夠還原使用eject前的樣子嗎？ ->->-> `一旦執行eject，就無法還原`
<!--SR:!2023-06-14,193,250-->

#🧠  React：若執行npm run eject 的話，會有什麼樣的潛在問題？ ->->-> `新增加進來模組安裝依賴增加至package.json，有些部署平台無法正常安裝，這會導致無法進行建置或者在部署之前就測試正確、新增被隱藏的模組依賴至package.json並不會區分哪些開發的？哪些是原本被隱藏的？`
<!--SR:!2024-02-08,175,210-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@casieberReactjsWhatDoes]]
[[@facebookAvailableScriptsCreate]]