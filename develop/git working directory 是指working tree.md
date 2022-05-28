

## 描述

引用git 官方repo[[@gitsterGitFastScalable2022]]備註所說明的：

> "git status" used to say "working directory" when it meant "working tree"

當提到是working tree，會直接是指working directory

另外從以下討論串可以得知
- [[@stewartAnswerWorkingTree2016]]
- [[@thomsonAnswerWorkingTree2016]]
- [[@burghardtAnswerWorkingTree2016]]

> So this change was made to better disambiguate between the _working tree_, meaning the location where your repository has been checked out, and the _working directory_ where you are running the `git status` command, which may be somewhere beneath your working tree (or perhaps not, if you set `GIT_WORK_TREE` environment variable).

它會因而強調是為了不讓working tree 和 working directory之間有所誤解

## 總結
working tree 會等同於 working directory

## 複習

#🧠 working directory 和 working tree有什麼差別？ ->->-> `並不差別，兩者皆為一樣，只是tree特別以樹狀結構來強調著directory的結構`
<!--SR:!2022-06-05,8,250-->

---
Status: #📥 
Tags:
[[Git]]
Links:
[[git 有working tree、working directory、repository、staged area、index]]
References
[[@gitsterGitFastScalable2022]]
[[@stewartAnswerWorkingTree2016]]
[[@thomsonAnswerWorkingTree2016]]
[[@burghardtAnswerWorkingTree2016]]