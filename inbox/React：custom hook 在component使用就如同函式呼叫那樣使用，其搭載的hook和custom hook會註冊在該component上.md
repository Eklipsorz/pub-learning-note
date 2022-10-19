## 描述



### custom hook 如何在其他component使用

custom hook 使用上就跟函式一樣：
	- 呼叫：只要在元件上以函式來呼叫就能使用，但會間接替各個元件註冊對應hook在元件上面
	- 回傳：若要custom hook回傳的話，就直接像個函式那樣回傳，回傳型別可以是任意

```
  const useCounter = () => { 
	.
	.
	.
    return xxx
  }
```


### custom hook 在component 呼叫的話

custom hook 在component 呼叫的話，就等同在component註冊custom hook，此時custom hook和搭載其上面的hook會是：
- 若搭載其他hookA(含state)的hookB在componentA呼叫的話，其hookA和hookB也直接註冊在componentA上
- 若同個搭載其他hookA(含state)的hookB在多個component呼叫的話，每個component都會擁有各自的hookA和hookB註冊在他們身上，同個hook在多個component呼叫並不意味著他們共享著state和effect


#### 結論

多個元件使用同個hook的共享狀態會是：
- 共享hook上的業務邏輯
- 不共享state或者effect




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：定義 custom hook 以及注意事項]]
References: