## 描述


### noValidate 是對應form 元素的novalidate屬性
[[@JavascriptHowDisable]]
```
return (
    <form className={styles.form} onSubmit={cartSubmitHandler} noValidate>
      <NumberInput
        label='Amount'
        attr={{
          id: `meal-item-${props.id}`,
          type: 'number',
          min: '1',
          max: '5',
          step: '1',
          defaultValue: '1',
        }}
        ref={inputRef}
      />
      <button>+ Add</button>
      {!isValidAmount && <p>Please input a amount</p>}
    </form>
  );
```

### novalidate 作用
[[@HTMLChaoWenBenBiaoJiYuYanMDN]]
> This Boolean attribute indicates that the form shouldn't be validated when submitted.


0. 該屬性為屬於原生HTML DOM的form
1. 表單元件 form 擁有的屬性之一
2. 用途：
	- 關閉瀏覽器對於表格提交時的預設自動驗證功能
	- 關閉根據預設的自動驗證結果來呈現對應的樣式內容
3. 細節：
	- 若沒設定novalidate的話，瀏覽器預設上會在第一時間阻擋到沒通過驗證的情況並做處理。形式會是：
		- 以瀏覽器的自動驗證規則來驗證提交結果
		- 根據結果來渲染其樣式內容

```
<form novalidate>

</form>
```


## 複習

#🧠 novalidate 屬性是屬於React？還是原生HTML DOM ->->-> `屬於原生HTML DOM的form`

#🧠 原生HTML DOM的form：novalidate屬性用途為何？ ->->-> `		- 關閉瀏覽器對於表格提交時的預設自動驗證功能 - 關閉根據預設的自動驗證結果來呈現對應的樣式內容`

#🧠 原生HTML DOM的form：若沒設定novalidate屬性，其表格會發生什麼？ ->->-> `		- 以瀏覽器的自動驗證規則來驗證提交結果- 根據結果來渲染其樣式內容`

#🧠 原生HTML DOM的form： novalidate屬性是涉及哪個事件的驗證功能->->-> `表單提交事件`

#🧠  原生HTML DOM的form 如何設定novalidate 屬性 ->->-> `<form novalidate></form>`

#🧠 若要在React的表格添加novalidate屬性，該如何編輯才有對應屬性？ ->->-> `<form noValidate></form>`

#🧠  原生HTML DOM的form：若開發者另外開發驗證規則以及其規則，也沒設定novalidate，那麼瀏覽器會如何執行提交驗證？->->-> `會先以瀏覽器的預設規則來驗證和渲染其內容，並不會執行開發者另外開發的`

#🧠 原生HTML DOM的form：執行event.preventDefault()會關閉自動驗證嗎？ ->->-> `並不會，preventDefault只是單方面取消特定事件的預設事件處理。`

---
Status: #🌱 #📓 
Tags:
[[React]] - [[HTML]]
Links:
References:
[[@JavascriptHowDisable]]
[[@HTMLChaoWenBenBiaoJiYuYanMDN]]