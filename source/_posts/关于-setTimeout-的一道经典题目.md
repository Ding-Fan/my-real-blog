---
title: 关于 setTimeout 的一道经典题目
date: 2018-11-17 11:49:45
tags:
---

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i)
  }, 100)
}
// 3 3 3

console.log(i)
// 3

```

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i)
  }, 100)
}
// 0 1 2

console.log(i)
// ReferenceError: i is not defined

```

突然想 babel 转换后是什么样子，就试了下：

```js

var _loop = function _loop(i) {
  setTimeout(function () {
    console.log(i);
  }, 100);
};

for (var i = 0; i < 3; i++) {
  _loop(i);
}
// 0 1 2

console.log(i)
// 3

```

很有趣，这样就是 `_loop(0) _loop(1) _loop(2)` 了