## 描述


###
> where you can enter data in a form this is prevented by a prompt which is shown to you asking you if you really wanna navigate away.

  

> So that as soon as you started working on that form, you can't accidentally leave it and that's a behavior we also might want to implement

  

prevented by a prompt：

實現表單頁面離開前警告提示

###


first, we wanna determine when the user starts working with this form e.g., when this form gains focus.

  

second, we wanna show a warning to the user if he or she tries to leave the page after starting to working on that form

  

  

製作表單離開前的提示元件來告知使用者：

1. 要確定使用者何時開始使用表單，可用form focus來用

2. 當使用者想從表單頁面離開時就以警告來告知


###

first, we wanna determine when the user starts working with this form e.g., when this form gains focus.

實現會是使用 form focus事件

  

  

focus事件為特定元件轉變成active element的瞬間

  

The `**focus**` event fires when an element has received focus.

###

wanna store that info that's this form was focused

1. 為表單focus事件處理添加狀態

2. 當focus時就設定狀態為true

  

prompt component

1. 由react-router-dom所提供

2. 自動監測特定規則是否滿足，若滿足就呈現warning，若不滿足就不呈現。

3. Prompt 有兩個主要的attributes：

- when：布林值，true為使用prompt來阻止從目前頁面跳轉；false為不使用

> to finding whether this prompt should be shown if the user changes the URL or not

- message：字串或者function，主要是指定prompt的主體訊息是什麼，當使用function可以根據使用者對於瀏覽紀錄的操作和位置來定義後續處理，回傳內容正是指定prompt的主體訊息

=> (location, action) => {} 中的location 是指使用者當前要跳轉的頁面位置，action是指使用者當前對於瀏覽紀錄的操作是什麼

  

> this is a component which we can render. And then this component will automatically watch if we navigate away. And if then a certain condition is met, it will show a warning before it allows use to leave

  

Used to prompt the user before navigating away from a page. When your application enters a state that should prevent the user from navigating away (like a form is half-filled out), render a `<Prompt>`.


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: