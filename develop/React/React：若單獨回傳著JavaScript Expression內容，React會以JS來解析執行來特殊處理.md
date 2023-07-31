## 描述


若單獨回傳JS Expression 內容，React會直接以JS來解析執行來特殊處理，不用添加\{\}：在這裡會根據enable是否為true來決定最後渲染內容

```
function App() {
  const meals = DUMMY_DATA;
  const enable = false;
  
  return (
	enable ? <h2>enable</h2> : <h2>disable</h2>
  );
}
```

若將JS Expression當成陣列的其中一個元素，會先當作單獨回傳JS Expression的內容來做特殊處理，也就是以JS來解析
```
function App() {
  const meals = DUMMY_DATA;
  const enable = false;
  return (
    [
      enable ? <h2>enable</h2> : <h2>disable</h2>,
      <h2>others</h2>
    ]
  );
}
```

### 若破壞單獨回傳的話
若破壞單獨回傳的話，比如夾雜額外元素的話，會使React不以特殊處理來解析原本的JS Expression：
	- JS Expression 一部分會變成一般字串
	- JS Expression 一部分會變成JSX Element
```
function App() {
  const meals = DUMMY_DATA;
  const enable = false;
  
  return (
	<div>
		enable ? <h2>enable</h2> : <h2>disable</h2>
	</div>
  );
}
```

## 複習

#🧠 React：若單讀回傳JS Expression為渲染內容且沒添加\{\}的話，React會如何處理？->->-> `React會直接以JS來解析執行來特殊處理，不用添加\{\}：在這裡會根據enable是否為true來決定最後渲染內容`
<!--SR:!2024-10-14,454,250-->

#🧠 return ( enable ? \<h2\>enable\<\/h2\> : \<h2\>disable\<\/h2\>) 為React元件的渲染內容的話，會如何執行？ ->->-> `會直接以JS來解析執行，根據enable是否為true來決定最後渲染內容`
<!--SR:!2024-10-20,460,250-->

#🧠 React：若單獨回傳JS Expression為渲染內容且沒添加\{\}且還夾雜著其他元件的話，React還會進行特殊處理嗎？ ->->-> `並不會特殊處理`
<!--SR:!2023-11-08,216,230-->


#🧠 React：若單獨回傳JS Expression為渲染內容且沒添加\{\}且還夾雜著其他元件的話，React並不會特殊處理，那會怎麼處理？->->-> `- JS Expression 一部分會變成一般字串 - JS Expression 一部分會變成JSX Element`
<!--SR:!2024-12-10,498,250-->

#🧠 React：若單獨將JS Expression為渲染內容納入陣列的其中一個元素且沒添加\{\}的話，React會如何處理？ ->->-> `React會直接以JS來解析執行來特殊處理，不用添加\{\}：在這裡會根據enable是否為true來決定最後渲染內容`
<!--SR:!2024-10-17,457,250-->

#🧠 React：會讓React在渲染部分以JS Expression處理的途徑有哪些？ ->->-> `單獨回傳JS Expression、在渲染內容使用{}和JS Expression、陣列的其中一個元素擺放JS Expression`
<!--SR:!2023-08-04,195,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[boolean expression && JSX Element案例：混雜其他元件＋boolean expression && JSX Element 未放入到{} vs. 混雜其他元件＋boolean expression && JSX Element 放入到 {}]]
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
[[在渲染層面下，render 函式回傳的內容若單純添加boolean expression && JSX element 的話，會使其語法正常執行，反之在其基礎下添加其他元素的話，其語法會被視為字串和一般的React Element來看待]]

References: