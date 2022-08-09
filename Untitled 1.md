React allows you to create re-usable and reactive components consisting of HTML and JS (and CSS)

React Declarative Approach：
渲染目標為target state
如何告知目標

React 將會解讀目標而生成對應的渲染指令以及視情況調用開發者所製造的元件
	渲染指令-> actual DOM instructions


```
function App() {
	return (
		<div>
			<h2>Let's get started!</h2>
		</div>
	);
}
```

其中return和括號內分別為告知系統目標、目標是什麼