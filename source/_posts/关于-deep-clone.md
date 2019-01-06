---
title: 关于 deep clone
date: 2018-12-05 21:05:06
tags:
---

经常会遇到，对一个 [] 进行 for loop 的场景。然而遇到 [{}, {}, {}] 时，要小心。

```js
let hei = [{a: 1}, {a: 2}, {a: 3}]

for(let x of hei) {
  console.log(x) // {a: 1}, {a: 2}, {a: 3}
  let y = Object.assign({}, x)
  y.a += 1
  console.log(x) // {a: 1}, {a: 2}, {a: 3}
  console.log(y) // {a: 2}, {a: 3}, {a: 4}
  // 然后我们就可以用放心的使用 y 而不必担心 hei 被改变了
  // 但是！如果 hei 里面有 {a: { b: 1 }} 这样的东西的话。。。
  // 我们可以用 JSON.stringify
  // 如果为了保险，兼容更复杂的情况，就用 lodash 的 cloneDeep 吧
  // https://lodash.com/docs/4.17.11#cloneDeep
}

console.log(hei) // {a: 1}, {a: 2}, {a: 3}
```