## 描述

[[@mdnWhatURLLearn]]
> Examples of relative URLs

> To better understand the following examples, let's assume that the URLs are called from within the document located at the following URL: https:\/\/developer\.mozilla\.org\/en-US\/docs\/Learn

> Sub-resources

> Because that URL does not start with `/`, the browser will attempt to find the document in a subdirectory of the one containing the current resource. So in this example, we really want to reach this URL: https:\/\/developer\.mozilla\.org\/en-US\/docs\/Learn\/Skills\/Infrastructure\/Understanding_URLs.

```
Skills/Infrastructure/Understanding_URLs
```

> Going back in the directory tree

> ../CSS/display

> In this case, we use the `../` writing convention — inherited from the UNIX file system world — to tell the browser we want to go up from one directory. Here we want to reach this URL: https\:\/\/developer\.mozilla\.org\/en-US\/docs\/Learn\/\.\.\/CSS\/display, which can be simplified to: https\:\/\/developer\.mozilla\.org\/en-US\/docs\/CSS\/display.

```
../CSS/display
```

```
https://developer.mozilla.org/en-US/docs/CSS/display
```

重點：
- relative URL 會是以特定資源A的所在目錄位置為參考點來找到特定資源B的路徑，特定路徑A通常會是以特定資源A的所在目錄位置為參考點來指定，舉例來說：假如目前存取頁面是/path1/path2/file，那麼就會以頁面所在的位置/path1/path2為參考點
- 在這裡除了path以外，其餘的protocol、host、port會和目前存取頁面的路徑擁有的protocol、host、port一樣。
- 具體方式有兩種：
	- sub-resource：直接從當前頁面所在目錄找
	- Going back in the directory tree：以當前頁面所在目錄來位移
- sub-resource：直接從當前頁面所在目錄找
	- 以目前存取頁面的目錄所在路徑為參考點來找到
	- 路徑格式會是開頭不夾帶\/：假如目前頁面路徑為path1/file，那麼瀏覽器就會試著在path1下面找到dir這個目錄，然後再從那找到file。
```
dir/file
```
- Going back in the directory tree：以當前頁面所在目錄來位移
	- 以目前存取頁面的目錄所在路徑為參考點並透過位移來找到對應資源
	- 路徑格式通常會是\.\/或者\.\.\/為開頭：假如目前頁面路徑為path1/path2/file，那麼就會以path1/path2為參考點來位移，第一個則是朝著path1這目錄來找到file2，第二個則是以當前目錄所在來找到file2，也就是path2/file2
```
../file2
./file2
```

#### 案例
假設頁面路徑為
```
https://developer.mozilla.org/en-US/docs/Learn/hi.html
```

直接從當前頁面所在目錄找：它會直接從hi.html所在的目錄找到以下內容，也就是https:\/\/developer\.mozilla\.org\/en-US\/docs\/Learn\/Skills\/Infrastructure\/Understanding_URLs
```
Skills/Infrastructure/Understanding_URLs
```

以當前頁面所在目錄來位移：它會直接以hi.html所在的目錄路徑為參考點，也就是https:\/\/developer\.mozilla\.org\/en-US\/docs\/Learn為參考點，然後往前位移一個目錄，也就是https:\/\/developer\.mozilla\.org\/en-US\/docs\/，最後會是https:\/\/developer\.mozilla\.org\/en-US\/docs\/CSS\/display
```
../CSS/display
```


## 複習

#🧠 relative URL是什麼？->->-> `relative URL 會是以特定資源A的所在目錄位置為參考點來找到特定資源B的路徑，特定路徑A通常會是以特定資源A的所在目錄位置為參考點來指定`
<!--SR:!2024-09-07,389,230-->


#🧠 假如目前存取頁面是/path1/path2/file，那麼relative URL會以什麼做為參考點？ ->->-> `/path1/path2為參考點`
<!--SR:!2024-07-10,369,250-->

#🧠 relative URL 對於URL構造來說，其path、protocol、host、port會如何被決定 ->->-> `在這裡除了path以外，其餘的protocol、host、port會和目前存取頁面的路徑擁有的protocol、host、port一樣。`
<!--SR:!2023-08-30,190,250-->


#🧠 relative URL實現方式哪兩種？ ->->-> `直接從當前頁面所在目錄找、以當前頁面所在目錄來位移`
<!--SR:!2023-09-12,16,249-->

#🧠 relative URL： 直接從當前頁面所在目錄找， relative URL指定路徑格式會是什麼->->-> `路徑格式會是開頭不夾帶/`
<!--SR:!2024-12-16,474,250-->

#🧠  relative URL：路徑格式會是開頭不夾帶\/，舉一個路徑案例->->-> `dir/file`
<!--SR:!2024-11-06,447,250-->


#🧠 relative URL： 假如指定路徑為dir/file，且目前頁面路徑為path1/file，那麼瀏覽器如何找->->-> `假如目前頁面路徑為path1/file，那麼瀏覽器就會試著在path1下面找到dir這個目錄，然後再從那找到file。`
<!--SR:!2024-04-07,317,250-->


#🧠 relative URL： 以當前頁面所在目錄來位移，relative URL指定路徑格式會是什麼？->->-> `路徑格式通常會是./或者../為開頭`
<!--SR:!2023-09-14,150,230-->

#🧠  relative URL：以當前頁面所在目錄來位移，舉一個路徑案例 ->->-> `../file2 或 ./file2`
<!--SR:!2023-09-05,194,250-->



#🧠 假如目前頁面路徑為path1/path2/file，那麼瀏覽器面對\.\.\/file2和\.\/file2這些路徑會如何找？ ->->-> `假如目前頁面路徑為path1/path2/file，那麼就會以path1/path2為參考點來位移，第一個則是朝著path1這目錄來找到file2，第二個則是以當前目錄所在來找到file2，也就是path2/file2`
<!--SR:!2024-12-15,473,250-->

#🧠 假如目前頁面路徑為path1/path2/file，目前指定路徑為exampledir/example1，那麼瀏覽器會解析成path1/path2/file/exampledir/example1嗎？ 為什麼？->->-> `並不對，它會看頁面所在的目錄所在，也就是path1/path2，所以當指定路徑為exampledir/example1，那麼就是在path1/path2找到exampledir目錄，然後再從那找到example1，也就是path1/path2/exampledir/example1`
<!--SR:!2023-09-05,194,250-->


#🧠 假如目前頁面路徑為path1/path2/file，目前指定路徑為../dir1/example1，那麼瀏覽器會解析成path1/path2/dir1/example1嗎？ 為什麼？->->-> `並不對，它看頁面所在的目錄所在，也就是path1/path2，在這裡指定../，那麼就會在path1目錄找到dir1這目錄，然後從那找到example1，整體就是path1/dir1/example1`
<!--SR:!2023-09-02,192,250-->


#🧠 假設頁面路徑為https://developer.mozilla.org/en-US/docs/Learn/hi.html，請問當指定為Skills/Infrastructure/Understanding_URLs，會找到哪個位置？為什麼？->->-> `直接從當前頁面所在目錄找：它會直接從hi.html所在的目錄找到以下內容，也就是https://developer.mozilla.org/en-US/docs/Learn/Skills/Infrastructure/Understanding_URLs`
<!--SR:!2024-09-25,420,250-->

#🧠 假設頁面路徑為https://developer.mozilla.org/en-US/docs/Learn/hi.html，請問當指定為../CSS/display，會找到哪個位置？為什麼？->->-> `以當前頁面所在目錄來位移：它會直接以hi.html所在的目錄路徑為參考點，也就是https://developer.mozilla.org/en-US/docs/Learn為參考點，然後往前位移一個目錄，也就是https://developer.mozilla.org/en-US/docs/，最後會是https://developer.mozilla.org/en-US/docs/CSS/display`
<!--SR:!2024-09-18,413,250-->



---
Status: #🌱 
Tags:
[[Rendering]]
Links:
[[absolute URL：意指為特定資源在網路上的完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置]]
[[URL 種類具體有absolute URL 和 relative URL]]
References:
[[@mdnWhatURLLearn]]