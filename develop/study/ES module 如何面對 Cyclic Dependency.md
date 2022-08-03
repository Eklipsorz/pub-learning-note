## 描述

### 文獻1說明

#### **模块循环引用**
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]：
> 对于循环引用的场景，会先对子模块进行预处理和执行。连接阶段除了分析模块依赖关系，还会创建执行上下文和初始化变量，所以连接阶段主要包括分析模块依赖关系和对模块进行预处理。如图 9 所示，对于图 5 的模块关系，处理顺序为：预处理 B -> 预处理 A -> 执行 B -> 执行 A。

![](https://pic3.zhimg.com/80/v2-bf22b5c68ae1c3a4387f70665866d5e2_720w.jpg)
图 9

#### 使用不当的问题

> 于子模块先于父模块被执行，子模块直接执行从父模块导入的变量会导致 JS 错误。

```js
// 文件 parent.js
import {} from './child.js';
export const parent = 'parent';

// 文件 child.js
import { parent } from './parent.js';
console.log(parent); // 报错
```
代码 2

> 如代码 2 所示，child.js 中的导入变量 parent 被绑定为 parent.js 的导出变量 parent，当执行 child.js 的最后一行代码时，parent.js 还没有被执行，parent.js 的导出变量 parent 未被初始化，所以 child.js 中的导入变量 parent 也就没有被初始化，会导致 JS 错误。注意，本文说的变量是统称，包含 var、let、const、function 等关键字声明的变量。

```text
console.log(parent)
            ^

ReferenceError: Cannot access 'parent' before initialization
```


代码 3

重點：
- ES module 會使用環狀依賴結構的檢測方法來檢測，若為環狀依賴結構就於下列階段進行：
	- instantiation：
		- DFS post-order traversal 遍歷到環狀結構上最後一個未曾遍歷的模組就停止該方向的遍歷並以該模組為那個方向的最後一個模組
		- 不讓最後一個模組對環狀結構上的第一個遍歷到的模組進行import，由於第一個模組還未開始instantiation
	- evaluation：等待所有模組的instantiation都做完
		- DFS post-order traversal 遍歷到環狀結構上最後一個未曾遍歷的模組就停止該方向的遍歷並以該模組為那個方向的最後一個模組
		- 執行最後一個模組的加載來從module map獲取對應紀錄的記憶體位址來將模組之import識別字對應其記憶體位址
		- 執行最後一個模組的top-level code，通常若存取自第一個模組加載過來的識別字所對應的記憶體區塊會顯示以下訊息來表示其識別字的記憶體還未分配，而此時的第一個模組會因為等待最後一個模組執行完evaluation或者還未被挑到來執行evaluation
		```
		Cannot access 'x' before initialization
		```

- 舉例：假設有兩個JS模組分別為a.js和b.js，在這裏會先執行a.js，所以a.js會先依賴著b.js，b.js也隨後依賴著a.js，在這裏JS執行之前，會進入編譯分析階段來判斷依賴關係圖是否為環狀模組依賴關係，結果檢測結果是環狀模組依賴關係：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659516780/blog/javascript/module/es-module/cyclic-dependency-code-example_dvfifa.png)
	- instantiation：
		-  DFS post-order traversal 遍歷到b.js就停下，並以b.js為這個依賴方向的最後一個模組
		- 不讓b.js對環狀結構上的a.js進行import，因為a.js還未進行開始instantiation
	- evaluation：等待所有模組的instantiation都做完
		-  DFS post-order traversal 遍歷到b.js就停下，並以b.js為這個依賴方向的最後一個模組
		-  執行b.js對於a.js模組的加載，具體加載會是：從module map獲取對應紀錄的記憶體位址來將模組之import識別字對應其記憶體位址
		- 執行b.js模組上的top-level code，但結果由於a.js必須等待b.js執行完evaluation才能輪到它執行，所以b.js無法獲取自a.js引入的記憶體空間而報錯
		```
		ReferenceError: Cannot access 'a' before initialization		
		```

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659514781/blog/javascript/module/es-module/cyclic-dependency-digram-example_uupj04.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659514781/blog/javascript/module/es-module/cyclic-dependency-digram-example_uupj04.png)

#### 若產生非同步任務來處理evaluation
> 如果是异步执行，则没问题，因为异步执行的时候父模块已经被执行了。例如，代码 3 是能正常运行的。

```js
// parent.js
import {} from './child.js';
export const parent = 'parent';

// child.js
import { parent } from './parent.js';
setTimeout(() => {
  console.log(parent) // 输出 'parent'
}, 0);
```

重點：在這裏parent.js會是依賴著child.js，並先執行parent.js
- 那麼若在evaluation階段中，先讓JS引擎在child.js上產生非同步任務來印出parent.js所要輸出的識別字，是可以透過額外產出的任務在parent.js執行後才執行，並正確獲得對應記憶體內容

### 文獻2說明
[[@linclarkESModulesCartoon]] ：
> If the export were handled using live bindings, the counter module would see the correct value eventually. By the time the timeout runs, `main.js`’s evaluation would have completed and filled in the value.

> Supporting these cycles is a big rationale behind the design of ES modules. It’s this three-phase design that makes them possible.


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[在JS中，let和const 宣告會是包含著分配記憶體給識別字以及分配初始值至對應記憶體區塊]]
References:
[[@linclarkESModulesCartoon]]
[[@zijieqianduanShenRuFenXiJavaScriptMoKuaiXunHuanYinYong]]