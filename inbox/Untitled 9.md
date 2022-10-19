
## 描述


擁有deps
	- dependency 不需要添加更新狀態用的函式：因為React本身和使用者本身就不會變動該函式本身，且無法代表目前元件的互動狀態
	- dependency 不要添加其他非React能夠支援的API 或者對應函式：因為他們本身就不會改變，且無法代表目前元件的互動狀態
	- dependency 不要添加屬於其他元件或者元件以外的變數/函式，因為它們本身就屬於其他元件或者非元件，它們一改變這件事本身就無法代表目前元件的互動狀態。

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
References: