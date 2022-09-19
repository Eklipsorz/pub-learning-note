## 描述


### html-webpack-plugin 用途
[[@royaWebpackQianDuanDaBaoGongJuShiYong2020]] 所描述：
> 在之前介紹 Webpack 的各種 loader 時，最後都得手動生成 HTML 文件並引入相關的靜態檔案，這樣不是很矛盾嗎？Webpack 可是自動化工具阿！怎會有這麼個缺陷？
> 
> html-webpack-plugin 可以幫助我們指定任意的 HTML 模板，並透過傳遞選項方式，生成對應的 HTML 文件，同時也會將 entry 內的所有靜態文件做引入動作，解決手動引入的困擾

> The [`HtmlWebpackPlugin`](https://github.com/jantimon/html-webpack-plugin) simplifies creation of HTML files to serve your webpack bundles

重點：
- html-webpack-plugin 沒出現前，webpack會有以下問題：
	- 手動生成HTML來當前端框架參考的模板網頁
	- 手動替模板文件載入webpack處理後的模組檔案
- html-webpack-plugin 為了以上問題而提出
	- 利用特定模板語言來方便生成前端框架參考的模板網頁
	- 替模板文件自動載入webpack處理後的模組檔案

### html-webpack-plugin 設定
[[@royaWebpackQianDuanDaBaoGongJuShiYong2020]] 描述：
> 配置 `webpack.config.js` 檔案：
```
const path = require('path');  
const MiniCssExtractPlugin = require('mini-css-extract-plugin');  
// 載入 html-webpack-plugin (第一步)  
const HtmlWebpackPlugin = require('html-webpack-plugin');  
  
module.exports = {  
  entry: './src/main.js',  
  output: {  
    path: path.resolve(__dirname, 'dist'),  
    filename: 'static/js/[name].[hash].js',  
  },  
  module: {  
    rules: [  
      {  
        test: /\.css$/i,  
        use: [MiniCssExtractPlugin.loader, 'css-loader'],  
      },  
    ],  
  },  
  plugins: [  
    new MiniCssExtractPlugin({  
      filename: 'static/css/[name].[hash].css',  
    }),  
    // 創建實例 (第二步)  
    new HtmlWebpackPlugin({  
      // 配置 HTML 模板路徑與生成名稱 (第三步)  
      template: './src/index.html',  
      filename: 'index.html',  
    }),  
  ],  
};  
```

> 我們可以刻意的將打包後的靜態檔案指定放置在不同的資料夾下，同時也須配置 html-webpack-plugin 的 `templete` 與 `filename`選項，`templete` 選項可將我們 `src/index.html` 檔案作為模板文件，簡單來講就是自動引入靜態檔案的目標文件，而 `filename` 選項則是用來配置目標文件生成時的名稱。

重點：
- 其中template會是指定哪個檔案作為模板文件以及作為自動加載webpack的產物的文件

## 複習
#🧠 在html-webpack-plugin 出現之前，webpack會有哪些問題？->->-> `	- 手動生成HTML來當前端框架參考的模板網頁 - 手動替模板文件載入webpack處理後的模組檔案`
<!--SR:!2022-11-14,60,250-->

#🧠 html-webpack-plugin 為了手動生成HTML來當前端框架參考的模板網頁、手動替模板文件載入webpack處理後的模組檔案而提出，那麼具體他會有何用途？->->-> `	- 利用特定模板語言來方便生成前端框架參考的模板網頁- 替模板文件自動載入webpack處理後的模組檔案`
<!--SR:!2022-12-02,74,250-->

#🧠 html-webpack-plugin所設定的template會對react.js有何幫助？ ->->-> `- 利用特定模板語言來方便生成前端框架參考的模板網頁 - 替模板文件自動載入webpack處理後的模組檔案`
<!--SR:!2022-11-20,66,250-->

---
Status: #🌱 
Tags:
[[webpack]] - [[JavaScript]]
Links:
References:
[[@royaWebpackQianDuanDaBaoGongJuShiYong2020]]