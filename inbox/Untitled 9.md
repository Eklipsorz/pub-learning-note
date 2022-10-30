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

重點：
- relative URL 會是以特定路徑為參考點來指定特定資源的路徑，特定路徑通常會是以目前存取頁面的所在路徑為參考點來指定
- 具體方式有兩種：
	- sub-resource
	- Going back in the directory tree
- sub-resource：
	- 會是以目前存取頁面的所在路徑
	- 格式會是開頭不夾帶\/


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
[[absolute URL：意指為特定資源在網路上的完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置]]
References:
[[@mdnWhatURLLearn]]