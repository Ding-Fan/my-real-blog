---
title: vue filter in ternary operator
date: 2019-01-09 11:58:31
tags:
---

没有图片时要显示占位图，所以在 `:src` 里用到了 ternary operator 。大概长这样：

```js
:src="picture ? (picture | imgShow) : require('../../assets/images/placeholder.png')"
```

然后报错了。于是查了 Vue filter 的用法 https://github.com/vuejs/vue/issues/5449

> The expression syntax is defined as (JavaScript expression) + (| filters). Filters can only be appended to valid JavaScript - bringing in filters into JavaScript is not going to happen.
>You can already use $options.filters.myFilter(prop) in JavaScript expressions.

所以正确用法是：

```js
              :src="picture ? $options.filters.imgShow(picture) : require('../../assets/images/placeholder.png')"
```

- 为什么要用 `require`

好像是 webpack 的相应的 loader （在我这里是 file loader ）要对这些 path 做一个转换操作。

- 我看 `console.log(this.$options)` 里没有 `filters` 啊

顺着 `__proto__` 就能找到了。。。