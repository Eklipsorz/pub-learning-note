## 描述


### html-webpack-plugin 用途

> html-webpack-plugin 可以幫助我們指定任意的 HTML 模板，並透過傳遞選項方式，生成對應的 HTML 文件，同時也會將 entry 內的所有靜態文件做引入動作，解決手動引入的困擾


### html-webpack-plugin 設定
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

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: