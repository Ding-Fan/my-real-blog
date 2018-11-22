---
title: 关于 JavaScript 里使用 flag variable 和 ==
date: 2018-10-30 19:27:09
tags:
---

tldr ：不要无脑使用 `==` 和 flag variable ，没想明白为什么要用，那就不要用。

编辑页面和新增页面几乎一模一样，我打算放在同一个页面里，进入页面的时候传入一个值作为 flag 。那么保存按钮就要根据该 flag 执行不同的功能。我一开始打算通过 url 传 `?isEdit=true` ，觉得比较直观，结果拿到传入的 `'true'` 后发现

```js
'true' == true
// false
```

[查资料](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Using_the_equality_operators) 后发现，首先 Boolean `true` 被转成了 Number `1` ，然后 String `'true'` 被转成了 Number `NaN`

```js
1 == true
// true

isNaN('true')
// true

NaN == 1
// false

'false' == false
// false
```

同事说：还是得用 0 1 哈哈哈哈。尝试了下，结果发现

```js
'0' ? 666 : 999
// 666

'0' == false
// true

!!'0' == true
// true
```

我意识到这是个大坑，决定尽量避免使用 `==` 。 **但是** 有些时候 `==` 是很有用的。例如调用 API 时，对返回的 statusCode 进行判断。后端返回的 statusCode 可能是 Number ，也可能是 String 。

```js
if(statusCode == 200) {

}
```

最终我决定传 `?isEdit=Y` 。通过判断 `isEdit === 'Y'` 去执行不同功能。这里的 `isEdit` 就是一个 flag variable 。通常我们会用 flag variable 作为 if 语句的判断条件。当 flag variable 的 value 就是 Boolean 时，可以直接用

```js
let theFlag = true

if(theFlag) {

}
```

有时就像 isEdit 一样

```js
let isEdit = 'Y'

if(isEdit === 'Y') {

}
```

滥用 flag variable 会导致成堆的 if ，就会成为传说中的 spaghetti code 。尽量把逻辑判断的代码和实际业务操作的代码解耦。在 _Clean Code_ 中也有这样一段

> Boolean arguments loudly declare that the function does more than one thing. They are confusing and should be eliminated.

参考：

- https://softwareengineering.stackexchange.com/questions/147977/is-it-wrong-to-use-a-boolean-parameter-to-determine-behavior
- https://www.wikiwand.com/en/Cohesion_(computer_science)
- https://www.wikiwand.com/en/Coupling_(computer_programming)
- https://softwareengineering.stackexchange.com/a/364562
- http://www.informit.com/articles/article.aspx?p=1392524
- https://www.wikiwand.com/en/SOLID