

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


set style of an element dynamically

使用對著對應元件上增加style屬性(attributes)

  

這屬性名稱分別有，兩者皆有不同：

1.  原生HTML DOM也有實現對應style屬性(attribute)
    
2.  React體系
    

  

第一個

The `style` attribute specifies an inline style for an element. 舉例：

`<h1 style="color:blue;text-align:center">This is a header</h1>`

  

第二個：

style屬性值

`<Component style={object} />`

  

object 會以{}來表示，其屬性名稱和屬性值會搭配css樣式下的屬性名稱和屬性值，設定方式有兩種：

- 使用字串來表示
```
<Component style={{'background-color': 'red'}} />
```
- 使用JS表示屬性的方式，但要使用lower camel case
```
<Component style={{backgroundColor: 'red'}} />
```



```
import './ChartBar.css';

function ChartBar(props) {
  const { value, label, maxValue } = props;
  let barFillHeight = '0%';

  if (maxValue > 0) {
    barFillHeight = Math.round((value / maxValue) * 100) + '%';
  }

  return (
    <div className='char-bar'>
      <div className='chart-bar__inner'>
        <div
          className='chart-bar__fill'
          style={{ height: barFillHeight }}
        ></div>
      </div>
      <div className='chart-bar__label'>{label}</div>
    </div>
  );
}

export default ChartBar;
```