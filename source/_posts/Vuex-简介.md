---
title: Vuex 简介
date: 2019-01-06 13:24:10
tags:
---

看了一个 [视频](https://youtu.be/_2_C9j-8CtM) 。

- **Vuex 是一个 State Management Pattern + Library 。**

我们把 Component 用到的东西放在 Vuex Store 的 state 里。用 actions 去调用 mutations 去修改 state 。用 getters 去取用 state 里的东西给 Component 用。

- **这样有什么好处？**

我有一个 Component A 和（它的爸爸的邻居的爷爷的孙子的弟弟） Component B 用到了一堆相同的东西。现在不用费心如何把 Component A 里的操作告知 Component B 了。

- **真香！那我全都放在 Vuex Store 里吧！**

当然没问题。事实上面对着诡异多变的需求，我是倾向于这样做的。谁能想到某一天 Component A 被要求关联看上去毫无交集的 Component G 呢？ Store once, use everywhere! 但是使用 Vuex 毫无疑问会增加代码量。我目前的解决方案是安装 Vuex Snippet 的插件或根据当前项目自己写 snippet 。

2019.01.04： 现在认为，在不同的情况下选择不同的方法或模式，就像在不同的语境下用不同的词法句式一样。

延伸阅读： [Should I Store This Data in Vuex?](https://markus.oberlehner.net/blog/should-i-store-this-data-in-vuex/)