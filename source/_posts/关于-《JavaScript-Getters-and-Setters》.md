---
title: 关于 《JavaScript Getters and Setters》
date: 2018-10-28 21:28:57
tags:
---

注意：建议直接看原视频。
[视频链接](https://youtu.be/bl98dm7vJt0)

在 JavaScript 中，一个 Object 长这样:

```js
const person = {
  firstName: 'Ding',
  lastName: 'Fan'
}
```

当我们想看全名时，可以这样：

```js
console.log(person.firstName + ' ' + person.lastName)
```

或者

```js
console.log(`${person.firstName} ${person.lastName}`)
```

每次想看全名都像这样有点麻烦，可以写成一个 method

```js
const person = {
  firstName: 'Ding',
  lastName: 'Fan',
  fullName() {
    return `${person.firstName} ${person.lastName}`
  }
}

console.log(person.fullName())
```

下面精彩的来了。

```js
const person = {
  firstName: 'Ding',
  lastName: 'Fan',
  get fullName() {
    return `${person.firstName} ${person.lastName}`
  },
  set fullName(value) {
    const parts = value.split(' ')
    this.firstName = parts[0]
    this.lastName = parts[1]
  }
}

person.fullName = 'Gintoki Sakada'

console.log(fullName)
```

现在我们可以用 `person.fullName` 去看全名，也可以用它去改变 `person` 。好耶！