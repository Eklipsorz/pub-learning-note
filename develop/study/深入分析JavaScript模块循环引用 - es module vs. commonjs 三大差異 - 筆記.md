## 描述

[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]
> ECMAScript 6 入门教程》一书说的三个重大差异如下：
> 1.  CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。  
> 2.  CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。  
> 3.  CommonJS 模块的`require()`是同步加载模块，ES6 模块的`import`命令是异步加载，有一个独立的模块依赖的解析阶段。  
    
> 对于第 1 点，CommonJS 和 ES6 模块输出的都是变量，变量都是值的引用。该章节的评论中也有人质疑这个点。
> 
> 对于第 2 点，前半句基本正确，后半句基本错误。CommonJS 模块在执行阶段加载子模块文件，ES6 模块在预处理阶段加载子模块文件，当然 ES6 模块在执行阶段也会加载子模块文件，不过会使用预处理阶段的缓存。从形式上看，CommonJS 模块整体导出一个包含若干个变量的对象，ES6 模块分开导出单个变量，如果只看父模块，ES6 模块的父模块确实在预处理阶段就绑定了子模块的导出变量，但是预处理阶段的子模块的导出变量是还没有被赋最终值的，所以并不能算真正输出。
> 
> 对于第 3 点，CommonJS 模块同步加载并执行模块文件，ES6 模块提前加载并执行模块文件。异步通常被理解为延后一个时间节点执行，所以说成异步加载是错误的。


重點：
- 完整加載會是：
	- 找到模組檔案並解析內容
	- 於記憶體建立區塊來打造模組實例
	- 在對應實例所在的記憶體區塊儲存模組所要提供的實際值
	- 將模組實例提供其他模組來使用或者其他主程式使用
- 第二點的話：
	- ES module：是透過編譯將export和/import的識別字對應其記憶體區塊，但記憶體區塊內容還沒有進行evaluation來賦予最終值，因此並不能夠說在編譯期間加載成功，而且還要考慮cyclic dependency問題，所以最後會於執行evaluation來重新加載和確定值，才能算完整的加載，因此會是 **ES module會是於編譯期間進行初步的記憶體對應，並於執行期間透過執行模組內容來完成加載** 。
- 第三點的話：
	- CommonJS：
	- ES module：是在編譯期間空出一些時間進行加載
## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]