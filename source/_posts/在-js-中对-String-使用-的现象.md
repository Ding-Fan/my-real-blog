---
title: 在 js 中对 String 使用 += 的现象
date: 2018-08-26 23:09:04
tags:
---

```js
let a = '300';
let b = '$';
// if we use a += b
// then a is '300$'

// if we use a = b + a
// then a is '$300'
```

在 js 中对 String 使用 += 时，请务必注意，可能结果并不是你想要的顺序，比如上面例子里的 `'300$'`
