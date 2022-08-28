

chart 元件分成 chart 本身和 顯示每個月開支的chartbar

chart 本身：Chart.js
ChartBar ： ChartBar.js


由Chart.js負責傳遞每個月的資訊至ChartBar.js元件，由該元件渲染指定月份的畫面



第一層div裡面分別有圖表欄(圖)和圖表欄位標籤這兩個區塊

圖表欄(圖)：具體是用完整bar想呈現哪一個區塊是未填滿的bar部分 以及 哪一個區塊是填滿的bar部分
圖表欄位標籤：則是以標註著這個bar是代表什麼資料
```
	<div className="chart-bar__inner">
		<div className="chart-bar__fill" />
	</div>
```


```
<div className="chart-bar">
	<div className="chart-bar__inner">
		<div className="chart-bar__fill" />
	</div>
	<div className="chart-bar__label">{props.label}</div>
</div>
```