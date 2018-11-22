---
title: get url parameters with javascript
date: 2018-11-21 23:20:38
tags:
---

写小程序时，扫描普通链接二维码，获取的参数是整个链接。记得 Vue 有直接从 `$route` 拿 `params` 的做法，然后还有 `window.location` 。有没有办法可以直接处理这样的 url String 呢？感觉用 `regex` 或 `split` 太粗暴，应该有现成的工具可用。搜索了几个都是粗暴的方式，终于找到一个 [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 看了看方法挺多，但是不支持 ie 。可达鸭抱头.jpg

最终我用了 `.split('?')[1].split('=')[1]` 。应该写个简单的 helper ？
<!-- 
```js
function myURL(url) {

}
``` -->

找到一个 [URI.js](https://github.com/medialize/URI.js) 。平时用的话还是手写或用自己的 helper 吧。