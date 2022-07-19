


## 描述
> ###成长期：模块化的雏形 - IIFE（语法侧的优化）
> ###作用域的把控

```
let count = 0;

const increase = () => ++count;

const reset = () => {
	count = 0;
}

increase();
reset();
```

> 利用函数块级作用域
```
() => {
	let count = 0;
}
```
  
> 仅定义了一个函数，如果立即执行
```
(() => {
	let count = 0;
})();
```

> 初步实现了一个最简单的模块
```
const iifeModule = () => {

	let count = 0;

	return {

		increase: () => {
			++count;
		},

		reset: () => {
			count = 0;
		}
	};

}

iifeModule.increase();
iifeModule.reset();
```
## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-07-22,3,250-->

---
Status: 
Tags:
Links:
References: