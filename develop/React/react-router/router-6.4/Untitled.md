## 描述


### 
> you also sometimes wanna find out what the current state of the data submission is because whilst we do redirect after data was submitted. we don't do anything whilst the data is being submitted.

  

確保一旦提交就不會有額外的提交內容，手段可以是：

1. 一旦提交就關閉提交按鈕

###

useNavigation：

1. 主要回傳目前router所攔截到navigation 操作/請求的目前狀態資料，包含導向狀態、導向的目的地、請求內的body部分

  

導向狀態有：

1. idle：表示目前沒任何navigation請求要做

2. submitting：表示目前攔截到提交時的navigation操作並做著對應的action

3. loading：表示目前攔截到目前router正執行loader來準備資料來給予對應元件做渲染

  

This hook tells you everything you need to know about a page navigation to build pending navigation indicators and optimistic UI on data mutations.

  

#### `navigation.state`

-   **idle** - There is no navigation pending.
    
-   **submitting** - A route action is being called due to a form submission using POST, PUT, PATCH, or DELETE
    
-   **loading** - The loaders for the next routes are being called to render the next page

## 複習
---
Status: #🌱 
Tags:
[[React]]
Links:
References: