---
title: safely accessing deeply nested values
date: 2018-11-22 10:50:23
tags:
---

比如你有一个 Object 叫 `haha` ，你要把 `haha.a.b.c.d` 的值取出来做一些事情。但是 `haha haha.a haha.a.b haha.a.b.c` 都有可能是 `undefined` 。

通常我的做法是：

```js
let d = ((((haha || {}).a || {}).b || {}).c || {}).d

if(d) { ... }
```

这样写太麻烦了。

> 不是有 proxy 大法么

查了 MDN 发现可以这样：

```js
let haha = {}

const handler = {
  get: function(target, prop, receiver) {
    return (target || {})[prop]
  }
}

const theProxy = new Proxy(haha, handler)
```

**但是** 这样并不能安全的用 `haha.a.b.c` ，需要让 `handler` 的 `get` 去`return` 一个 `new Proxy` 才行。

```js
let haha = {}

const handler = {
  get: function(target, prop, receiver) {
    return (target || {})[prop] || new Proxy({}, handler)
  }
}

const theProxy = new Proxy(haha, handler)
```

**但是** 这样的话， `haha haha.a haha.a.b haha.a.b.c` 全都是 `{}` 了。

> 这种情况还是直接 try 吧🌚

```js
let haha = {}
let goodYeah
try {
  goodYeah = haha.a.b.c
  
} catch (error) {
  goodYeah = undefined
}
```

好耶！ try 真香。
据说可以结合 `eval()` 使用。

> ?. 请

这是什么东西？一个问号一个点，没见过啊。搜索后得知 [proposal-optional-chaining](https://github.com/tc39/proposal-optional-chaining) 。是个（当前为） stage-1 的 proposal 。看 issue 里还有很多讨论，包括该用 `?.` 还是 `.?` 。

> 等 ?. 啊（

> 一般来说，我能等，但产品等不及