## 描述
[[@chenxuqinghymanXieReactDeShiHouChangChangTingDao2018]]
> Immutable 中文翻譯為**不變的**，簡單來說，我們每次操作 React state 的時候，原本的 state 是不變的，有變更到的物件記憶體位置要與原本的記憶體位置不同。

> -   React底層源碼有防呆機制，如果今天useState的資料為物件，則要注意物件是傳址不是傳值，所以要想辦法劃分新的記憶體空間儲存新陣列，讓React知道現在的資料是新的位址不是原本的位址。


重點：
- 若useState 或者 state 是以物件為主的話，會以每次的記憶體位址不同才會更改狀態，若相同的話，就會認為相同而不更新和觸發，換言之，若在同一個物件上增加屬性，並依此來要求更新狀態的話，會因為增加前和增加後的物件記憶體位置都一樣而不允許更新和觸發
```
setState(object)
```
- 解決辦法為：
	- 重新建立新個物件來存放舊狀態和新狀態，並將新物件指定為setState要更新的狀態
	```
	setState(newObject)
	```


### 範例1

在這裡，由於users在新增前和新增後都是一樣的記憶體位址，所以會被系統認為沒變動而不更新和觸發
```
  const [users, setUsers] = useState(initUsers);
  const itemAddHandler = (data) => {
    const callback = (users) => {
      const newUsers = users;
      newUsers.unshift(data);
      return newUsers;
    };
    setUsers(callback);
  };
```

解法為：
```
  const itemAddHandler = (data) => {
    const callback = (users) => {
      return [data, ...users];
    };
    setUsers(callback);
  };
```

## 複習

#🧠 若useState 或者 state 是以物件為主的話，會以什麼來區分狀態是否改變才會觸發更新和渲染？->->-> `依據著物件所在的記憶體位址是否相同，若相同就代表沒改變，若不相同就代表改變`
<!--SR:!2024-02-10,320,250-->


#🧠 若useState 或者 state 是以物件為主的話，會是以狀態的不同來區分是否改變，那麼不同會如何？相同又是如何？ ->->-> `相同的話，會不允許更新狀態和觸發；不同的話，允許更新狀態和觸發`
<!--SR:!2025-02-06,529,250-->


#🧠 若狀態為一個物件，並於同一個物件上增加屬性，並依此來要求更新狀態的話，要怎麼做才能確實更新狀態 ->->-> `重新建立新個物件來存放舊狀態和新狀態，並將新物件指定為setState要更新的狀態`
<!--SR:!2024-11-29,503,250-->

#🧠 React：請問這能正常渲染出新增的項目嗎？ 為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662403267/blog/react/state/object-wrong-useState-example_jwtgvz.png) ->->-> `不能，由於狀態是以物件為主，所以會以參照位址的不同來區分是否狀態改變，若不一樣就狀態改變；反之，若一樣就狀態不改變，在這裡是屬於後者，使用相同的記憶體位址來增加新元素。`
<!--SR:!2024-09-23,440,250-->

#🧠 React：以下程式碼不能夠渲染出新增的項目，請問如何改善，才能秀出新增的內容？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662403267/blog/react/state/object-wrong-useState-example_jwtgvz.png)->->-> ``
<!--SR:!2023-12-28,291,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactReact2022]]
[[@chenxuqinghymanXieReactDeShiHouChangChangTingDao2018]]