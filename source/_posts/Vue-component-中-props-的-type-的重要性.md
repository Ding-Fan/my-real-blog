---
title: Vue component 中 props 的 type 的重要性
date: 2019-01-16 11:09:01
tags:
---

使用 Element UI 中的上传组件时，报了个诡异的错

```js
[Vue warn]: Error in nextTick: "TypeError: Cannot create property 'uid' on string ''"
```

毫无头绪，搜索引擎也找不到结果。最后顺着文件一点点找，发现是 Element UI 的 fileList 要求是 Array 里放 Object ，但我传进去的是 Array 里放 String 。

