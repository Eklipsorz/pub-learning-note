

git 系統當中，有三個主要的空間名詞，
- working directory
- working tree
- repository

引用git 官方repo備註所說明的：

> "git status" used to say "working directory" when it meant "working tree"

當提到是working tree，會直接是指working directory


> So this change was made to better disambiguate between the _working tree_, meaning the location where your repository has been checked out, and the _working directory_ where you are running the `git status` command, which may be somewhere beneath your working tree (or perhaps not, if you set `GIT_WORK_TREE` environment variable).

它會因而強調是為了不讓working tree 和 working directory之間有所誤解

---
Status: #📥 
Tags:
Links:
References
