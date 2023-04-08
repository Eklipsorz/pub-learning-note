


## 描述
引用[[@michaelborgwardtPHPWhatDoes]]所描述：
> It means the function will work correctly when you pass it arbitrary binary data (i.e. strings containing non-ASCII bytes and/or null bytes).

引用[[@xiadayuErJinZhiAnQuanBinarySafe]]所描述的：
> _二进制安全功能（binary- safe function）是指在一个二进制文件上所执行的不更改文件内容的功能或者操作。这能够保证文件不会因为某些操作而遭到损坏_


> 因为有了对字符串长度定义len, 所以在处理字符串时候不会以零值字节(\0)为字符串结尾标志.
> 二进制安全就是输入任何字节都能正确处理, 即使包含零值字节.

重點：
- Binary-safe 為強調二進制內容不受到傷害，通常Binary-safe是形容函式、功能
- Binary-safe function 則是說明函式在處理以二進制為主內容(含字串和數字)的過程中會以二進制形式來處理，並不會以特殊格式來看待內容來處理，進而破壞二進制內容
- 即使輸入內容從顯示上來看是非二進制，但由於能夠在電腦呈現的形式是以二進制，所以仍會將其看待為二進制來處理


### 命名緣由
Binary-safe 中的Binary是二進制內容，而safe則是安全、不受影響、傷害，兩者合併再一起就是強調二進制內容不受傷害，通常Binary-safe是形容函式、功能
> **not harmed or damaged**


## 複習

#🧠 Binary-safe 是什麼意思？binary? safe?  ->->-> `Binary-safe 中的Binary是二進制內容，而safe則是安全、不受影響、傷害，兩者合併再一起就是強調二進制內容不受傷害，通常Binary-safe是形容函式、功能`
<!--SR:!2024-07-18,469,250-->

#🧠 Binary-Safe function 是什麼？ ->->-> `Binary-safe function 則是說明函式在處理以二進制為主內容(含字串和數字)的過程中會以二進制形式來處理，並不會以特殊格式來看待內容來處理，進而破壞二進制內容`
<!--SR:!2024-07-19,468,250-->

#🧠 Binary-Safe function 面對字串等非二進制為主的話，會如何處理 ->->-> ` 即使輸入內容從顯示上來看是非二進制，但由於能夠在電腦呈現的形式是以二進制，所以仍會將其看待為二進制來處理`
<!--SR:!2023-07-12,95,230-->

---
Status: #🌱 
Tags: [[Binary]]
Links:
[[Redis 面對String 會以Binary-safe來處理，這表示它會以二進制格式來看待String]]
References:
[[@michaelborgwardtPHPWhatDoes]]
[[@xiadayuErJinZhiAnQuanBinarySafe]]