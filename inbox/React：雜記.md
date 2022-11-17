## 描述

### 在實際表格呈現來說，使用者要做什麼才能讓讓系統判定表格是非法內容？

判斷擁有錯誤內容的輸入欄的條件：
-   得先觸碰 (isTouched?)
-   內容出錯 (validity)

#### touched 設定方式會是以？
通常會是以對應輸入欄的Blur事件來設定觸碰(isTouched)

### hook 執行方式看起來是？
1. Custom hook 在functional component角度來看 會如同函式那樣呼叫
2. 以dom來看，則是hook註冊在特定dom節點，如綁定特定資訊至對應dom節點




## 複習

#🧠 React：在實際表格呈現來說，使用者要做什麼才能讓讓系統判定表格是非法內容？->->-> `-   得先觸碰 (isTouched?) -   內容出錯 (validity)`
<!--SR:!2022-11-30,25,250-->



#🧠 React：對於表格的輸入欄判斷錯誤非法內容條件會是什麼？若沒觸碰的話，錯誤是？ ->->-> `通常直接不認為是錯誤`
<!--SR:!2022-12-09,22,250-->


#🧠 React：通常如何設定輸入欄的觸碰(isTouched) ->->-> `通常會是以對應輸入欄的Blur事件來設定觸碰(isTouched)`
<!--SR:!2022-12-04,28,250-->

#🧠 React： hook 執行方式在看起來是什麼？(functional component 角度和dom角度)->->-> `1. Custom hook 在functional component層級來看 會如同函式那樣呼叫 2. 以dom來看，則是hook註冊在特定dom節點`
<!--SR:!2022-12-04,28,250-->

#🧠 React： hook 執行方式在functional component看起來是什麼？ ->->-> ` Custom hook 在functional component角度來看 會如同函式那樣呼叫`
<!--SR:!2022-12-04,28,250-->


#🧠 React： 假如useXXXX()會是印出XXXX，請問在functional component下若是以下面形式來執行useXXXX(); console.log('hi')  其執行順序和結果是？->->-> `會先執行useXXXX 在來執行console`
<!--SR:!2022-12-04,28,250-->

#🧠 React：以dom來看，則是hook註冊在特定dom節點，比如說 ->->-> `綁定特定資訊至對應dom節點`
<!--SR:!2022-11-29,24,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References: