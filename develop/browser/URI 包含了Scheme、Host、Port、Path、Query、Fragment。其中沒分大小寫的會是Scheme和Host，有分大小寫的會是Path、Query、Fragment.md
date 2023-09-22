## 描述

[[@WhyAreURLs]]
> URLs are not case-sensitive, only parts of them.  
> For example, nothing is case-sensitive in the URL `https://google.com`,

> With reference to [RFC 3986 - Uniform Resource Identifier (URI): Generic Syntax](https://www.rfc-editor.org/rfc/rfc3986)

> First, from [Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Locator), a URL looks like:

```
 scheme:[//host[:port]][/]path[?query][#fragment]
```

> (I've removed the `user:password` part because it is not interesting and rarely used)
> -   [`scheme`](https://www.rfc-editor.org/rfc/rfc3986#section-3.1):
> schemes are case-insensitive

> -   [`host`](https://www.rfc-editor.org/rfc/rfc3986#section-3.2.2):
> The host subcomponent is case-insensitive.

> -   [`path`](https://www.rfc-editor.org/rfc/rfc3986#section-3.3):
> The path component contains data...

>-   [`query`](https://www.rfc-editor.org/rfc/rfc3986#section-3.4):
> The query component contains non-hierarchical data...

> -   [`fragment`](https://www.rfc-editor.org/rfc/rfc3986#section-3.5):
> Individual media types may define their own restrictions on or structures within the fragment identifier syntax for specifying different types of subsets, views, or external references

> So, the `scheme` and `host` are case-insensitive.  
> The rest of the URL is case-sensitive.


### URI 包含了什麼？

```
 scheme:[//host[:port]][/]path[?query][#fragment]
```

URI包含了：
1. Scheme：網路協定
2. Host ：主機名稱
3. Port：主機埠號
4. Path：向主機索要的資源位置，其位置會是該主機下的完整路徑
5. Query：對於索要的資源進行額外的要求字串，以問號\?為開頭並用井字號\#作為結尾
6. Fragment：在Path 對應的主資源中，指定哪個部分為要真正擷取和使用的資源部分，會分大小寫，會用井字號\#當做開頭


### 是否區分大小寫

沒分大小寫：
1. Scheme
2. Host

有分大小寫：
1. Path
2. Query
3. Fragment
  


#### 為什麼scheme 、Host 大小寫不分
主要為了方便負責解析其位置的伺服器很好地處理解析

#### 除了scheme 、Host 以外會分的原因

[[@WhyAreURLs]]
```
 scheme:[//host[:port]][/]path[?query][#fragment]
 \____________________/\________________________/
        Location                 Data
```

> -   Location - The location has a canonical form, and is case-insensitive. Why? Probably so you could buy a domain name without having to buy thousands of variants.
    
> -   Data - the data is **used by the target server, and the application can choose what it means**. It wouldn't make any sense to make data case insensitive. The application should have more options, and defining case-insensitivity in the spec will limit these options.

剩下則是由主要應用伺服器來決定大小寫而區分




## 複習

#🧠 URI 包含了什麼？ ->->-> ` Scheme、Host、Port、Path、Query、Fragment`
<!--SR:!2023-12-06,85,210-->

#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，請問這分別是什麼意思？ ->->-> `1. Scheme：網路協定 2. Host ：主機名稱 3. Port：主機埠號 4. Path：向主機索要的資源位置，其位置會是該主機下的完整路徑 5. Query：對於索要的資源進行額外的要求字串 6. Fragment：在Path 對應的主資源中，指定哪個部分為要真正擷取和使用的資源部份`
<!--SR:!2024-05-10,318,250-->


#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，請問Query String通常會以什麼符號作為開頭和結尾->->-> `開頭會是用問號？結尾是用井字號`
<!--SR:!2023-09-24,191,250-->

#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，Query String對於URI會是什麼？ ->->-> `對於索要的資源進行額外的要求字串`
<!--SR:!2024-05-29,265,230-->

#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，Fragment對於URI會是什麼？ ->->-> `在Path 對應的主資源中，指定哪個部分為要真正擷取和使用的資源部分`
<!--SR:!2023-09-27,194,250-->

#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，哪些是否區分大小寫->->-> `1. Path 2. Query 3. Fragment`
<!--SR:!2024-12-01,451,250-->


#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，哪些是否沒區分大小寫 ->->-> `1. Scheme 2. Host`
<!--SR:!2025-01-06,472,250-->

#🧠 為什麼URI中的scheme 、Host 大小寫不分 ->->-> `主要為了方便負責解析其位置的伺服器很好地處理解析`
<!--SR:!2024-05-31,333,250-->


#🧠 除了scheme 、Host 以外的內容會分大小寫的原因 ->->-> `剩下則是由主要應用伺服器來決定大小寫而區分`
<!--SR:!2024-10-03,411,250-->

#🧠 URI 包含了Scheme、Host、Port、Path、Query、Fragment，那麼格式會是什麼？ ->->-> ` scheme:[//host[:port]][/]path[?query][#fragment]`
<!--SR:!2024-09-29,411,250-->


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@WhyAreURLs]]
[[@wangWangZhiURLYingWenDaXiaoXieShiFouYouChaiBie2015]]