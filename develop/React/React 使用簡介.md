

## 描述


```
// create a new react application
npx create-react-app <application>
cd <application>
// run development server
npm start
```

create-react-app：
1. 是一個工具，主要是用來做快速建構基礎的react application開發環境
2. 算是鷹架開發技術
3. 





當你準備好發佈到線上環境，執行 `npm run build` 會在 `build` 文件夾裡建立一個你的應用程式的最佳化版本，

目錄結構：
src folder 主要存放具體的原始碼，具體包含了定義react元件的代碼
public folder：主要存放不被編譯和優化的內容，主要會是靜態檔案，如圖片、css

> The `public` folder contains the HTML file so you can tweak it, for example, to [set the page title](https://create-react-app.dev/docs/title-and-meta-tags). The `<script>` tag with the compiled code will be added to it automatically during the build process.

build folder：主要存放其React 原始碼經過編譯和優化後的產物
> `npm run build` creates a `build` directory with a production build of your app.


### create-react-app

> If you've previously installed `create-react-app` globally via `npm install -g create-react-app`, we recommend you uninstall the package using `npm uninstall -g create-react-app` or `yarn global remove create-react-app` to ensure that npx always uses the latest version.

重點：
- 官方不建議將create-react-app套件安裝系統全域環境上
- 官方建議將create-react-app套件安裝至特定目錄下的區域環境，以供團隊使用共同版本的鷹架技術來方便建構。

在這裡我採用的是在特定目錄**react-builder**下建立區域性的npm package.json以利建立區域性的create-react-app，接著我在該目錄下以下列指令來建立鷹架環境
```
npx create-react-app <app>
```


### package.json

1. 以JSON形式來定義目前專案的性質、功能描述、作者、使用憑證、script、所需要的NPM套件是什麼，而這些NPM套件會是從NPM平台下載回來並設定為區域性質的套件。

2. 允許使用者使用語義化版本規則(semantic versioning)來描述每個所需套件的版本是什麼，換言之，就是用特定語法來定義每個所需套件的版本是什麼，通常這些規則只是定義專案所需的套件版本範圍是什麼

3. 可以方便與其他開發者分享以及重複使用

4. 每一次透過npm指令來對套件進行更新、下載、變更都會影響(獲取)著package.json的內容


### 鷹架？

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: