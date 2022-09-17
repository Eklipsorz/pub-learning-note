## 描述


the effect runs too often


```
1.  useEffect(() => {
2.      const identifier = setTimeout(() => {
3.          console.log('Checking form validity!');
4.          setFormIsValid(......);
5.      }, 500);

7.      return () => {
8.          console.log('CLEANUP');
9.          clearTimeout(identifier);
10.      };
11.  },[emailState, passwordState]);
```


潛在問題：
- 每一次email輸入欄位或者password輸入欄位有變動就會觸發執行effect


實際上來說只想關注在輸入欄位上的validity是否有變動

  
解法為從eamilState、passwordState取出validity 的部分作為變動的基礎


```
1.  const {isValid: emailIsValid} = eamilState;
2.  const {isValid: passwordIsValid} = passwordState;

4.  useEffect(() => {
5.      const identifier = setTimeout(() => {
6.          console.log('Checking form validity!');
7.          setFormIsValid(emailIsValid && passwordIsValid);
8.      }, 500);

10.      return () => {
11.          console.log('CLEANUP');
12.          clearTimeout(identifier);
13.      };
14.  },[emailIsValid, passwordIsValid]);
```
  
好處：
- 減少大量不必要的處理，集中在email和password的合法性是否變動


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References: