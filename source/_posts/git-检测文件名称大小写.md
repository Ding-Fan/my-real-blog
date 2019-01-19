---
title: git 检测文件名称大小写
date: 2019-01-18 17:05:16
tags:
---



部署项目的时候报错 `Content.js` 找不到。在本地检查发现命名是 `content.js` 。（为啥在本地没有报错？）将 c 改为 C 后，发现 `git status` 没有检测到文件变更。通过搜索得知，需要配置：

```bash
# 注意此处是错误示范，为什么错请继续看下去
git config core.ignorecase false
```

配完果然检测到新文件 `Content.js` 。马上 commit 后 push 上去了。

打算把这件事记录下来，于是多看了一会儿 https://stackoverflow.com/questions/17683458/how-do-i-commit-case-sensitive-only-filename-changes-in-git

大吃一惊！原来只是添加了 `Content.js` ，之前的 `content.js` 并没有删除！

继续看下去，原来 macOS 是 case-insensitive file system （TODO: search），难怪在本地没报错。

所以正确做法是用 `git mv`

现在我把

```bash
git config core.ignorecase true
# 然后复制 Content.js 的内容并把它删掉
# 然后
git add .
# 然后 新建一个 Content.js 把内容放进去
# 然后
git add .
# 然后就可以 commit 和 push 了
```

（最终我还是没用 `git mv`）