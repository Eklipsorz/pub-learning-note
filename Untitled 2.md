## 描述


資料和畫面寫在一塊的話，那麼就會是hard code

若要解決的話，可以將資料和畫面分離：
- 資料的出處：都源自於使用者所給予的、向後端發送的回應資料、假資料
- 初步的切分：
	- 使用{}：若要在React element 中添加JS表達式對應的值，可以使用{}並於內部添加JS表達式，就會優先執行JS表達式並將對應值替代表達式
	```
	<h2>{expression}</h2>
	```
	- expression 對應值能夠允許填入至element的型別是數字、字串，單純物件的話，會發生錯誤。
```
function ExpenseItem() {

	const expenseDate = new Date(2022, 8, 10);
	const expenseTitle = 'Car Insurance';
	const expenseAmount = 294.672;

  
	return (
		<div className='expense-item'>
			<div>{expenseDate.toISOString()}</div>
			<div className='expense-item__description'>
				<h2>{expenseTitle}</h2>
				<div className='expense-item__price'>{expenseAmount}</div>
			</div>
		</div>
	);

}
```
XML 資料和畫面分離的話，會使XML成為可填入資料的模板，而JavaScript負責獲取資料和輔助填入資料至模板

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: