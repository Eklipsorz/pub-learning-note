## 描述


資料和畫面寫在一塊的話，那麼就會是hard code

若要解決的話，可以將資料和畫面分離：
- 資料的出處：都源自於使用者所給予的、向後端發送的回應資料、假資料
- 初步的切分：
	- 使用{}：若要在React element 中添加{}並於內部添加JS表達式，這樣就會優先執行JS表達式並將對應值替代表達式
	```
	<h2>{expression}</h2>
	```
	- expression 對應值能夠允許填入至element的型別是數字、字串，單純物件的話，會發生錯誤。
```
function ExpenseItem() {

	return (
		<div className='expense-item'>
			<div>2022/08/10</div>
			<div className='expense-item__description'>
				<h2>Car Insurance</h2>
				<div className='expense-item__price'>294.672</div>
			</div>
		</div>
	);

}
```
XML 資料和畫面分離的話，會使XML成為可填入資料的模板，而JavaScript負責獲取資料和輔助填入資料至模板


### XML 在JSX 的識別
XML 在 JSX 語言裡，是算 JavaScript 語法延伸的一部分，所以部分由它代表的HTML語法可能會跟JavaScript 原生語法起衝突。


~~### {expression}：若expression在渲染畫面前是個非字串或者非數字的話~~
1.~~ 若expression在最終確定渲染畫面是個非字串或者非數字的話，會報錯~~
2. ~~若不是在最終確定渲染畫面的階段，可以以JS能接受的型別來傳輸/處理~~

## 複習

#🧠 在JSX語言的資料畫面分離中，XML和JS負責什麼？(模板？資料？業務邏輯) ->->-> `XML負責建立可填入資料的模板，而JavaScript負責獲取資料和輔助填入資料至模板和業務邏輯`
<!--SR:!2023-05-25,178,250-->

#🧠 在JSX語言的資料畫面分離中，XML負責什麼？->->-> `XML負責建立可填入資料的模板`
<!--SR:!2023-06-17,194,250-->

#🧠 在JSX語言的資料畫面分離中，JS負責什麼？ ->->-> `而JavaScript負責獲取資料和輔助填入資料至模板和業務邏輯`
<!--SR:!2023-06-04,183,250-->


#🧠 在JSX語言中，其語言中的XML算是JavaScript的什麼 ？->->-> ` JavaScript 語法延伸的一部分`
<!--SR:!2023-06-08,185,250-->


#🧠 在JSX語言中，使用XML來表達html元件以及其樣式，那麼其class識別字會不會和原生JavaScript的class產生衝突？ ->->-> `會，這是因為XML在JSX是JavaScript語法中的延伸部分。`
<!--SR:!2023-06-16,193,250-->

#🧠 React：假若在react element填上{}和在括號內部填上表達式的話，請問渲染順序會是如何->->-> `會先執行以{}和內部的表達式，接著把結果取代{表達式}所在的地方，最後在以結果渲染畫面`
<!--SR:!2023-12-27,106,230-->

#🧠 React：若畫面和資料寫在一塊的話，就相當於寫死在一塊，為了畫面和資料的分離，可以在單一畫面如何做才能實現？ ->->-> `在React element添加{}和表達式，並且表達式放在{}內部，由於資料本身就會是表達式，所以可以先將渲染外部做完處理並存放特定變數，由{變數}來在渲染那邊以結果來渲染，這樣就能做完簡單的分離`
<!--SR:!2023-06-10,99,210-->




#🧠  React：假若在react element填上{}和在括號內部填上表達式的話，請問若不是在最終確定渲染畫面的階段，表達式可以是什麼型別 ->->-> `若不是在最終確定渲染畫面的階段，可以以JS能接受的型別來傳輸/處理`
<!--SR:!2023-06-12,188,250-->


#🧠 如何將日期、標題、價格這三個資料分離出來？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660148304/blog/react/data-view-separation/before-simple-separation-result_mznm1z.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660148304/blog/react/data-view-separation/simple-separation-result_n7nkqb.png)`
<!--SR:!2025-03-06,567,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: