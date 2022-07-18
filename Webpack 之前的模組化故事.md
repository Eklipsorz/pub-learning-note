

## 描述



[[@fengyeJSMoKuaiHuaMaiLuo]] 所描述：
> ###幼年期：无模块化

> 1. 开始需要在页面中增加一些不同的js：动画、表单、格式化
> 2. 多种js文件被分在不同的文件中
> 3. 不同的文件又被同一个模板引用
> 4. script标签引入

> 文件分离是最基础的模块化第一步
> 
> 问题出现：
> - 污染全局作用域 => 不利于大型项目的开发以及多人团队的共建


重點：在還沒替JS進行模組化為主的開發時期
- 檔案分離：初步的模組化，將DOM Document 上的CSS、JS拆分成多個CSS檔案、多個JS檔案來讓DOM Document能夠重複使用
- 遇到問題：JS全域環境上的作用域污染問題
	- 背景：由於1個DOM Document為1個Window 物件所構成的DOM tree，而JS的全域環境是依照Window物件來決定，所以每個DOM Document 為 每個獨立的JS全域環境
	- 依賴於DOM Document 1的JS 並不會污染另一個DOM Document 2的JS 上的作用域 
	- 在同一個DOM Document 的JS 中的多個程式碼區塊會彼此污染同一個作用域
### 為何要

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[HTML]]  - [[JavaScript]]
Links:
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]
References:
[[@fengyeJSMoKuaiHuaMaiLuo]]