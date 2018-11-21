---
title: 含小数的 px 的显示问题
date: 2018-11-12 16:57:07
tags:
---

写小程序时使用的 CSS 单位是 `rpx` 。 [参见](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html)

> rpx（responsive pixel）: 可以根据屏幕宽度进行自适应。规定屏幕宽为750rpx。如在 iPhone6 上，屏幕宽度为375px，共有750个物理像素，则750rpx = 375px = 750物理像素，1rpx = 0.5px = 1物理像素。

`1rpx` 的 border 有时候显示不出来。常见于 iOS 机器上。同事说通常使用偶数的 `rpx` 。

我们常用的显示设备属于 raster display [参考](http://printwiki.org/Raster_Display) ，
我查了 MDN ， [`<length>`](https://developer.mozilla.org/en-US/docs/Web/CSS/length) 其中的 <number> 是可以有 fractional value 的。 [参见](https://developer.mozilla.org/en-US/docs/Web/CSS/number) 不同浏览器对 fractional value 有不同的处理方式。[参见](https://cruft.io/posts/percentage-calculations-in-ie/ )  既然如此，还能不能使用 fractional value 呢？有一个回答是：在用 percentage 时能，在直接写 `px` 时不推荐。 [参见](https://stackoverflow.com/questions/4308989/are-the-decimal-places-in-a-css-width-respected)  [参见](https://stackoverflow.com/questions/5581973/where-do-the-lost-pixels-go-in-a-percent-css-layout/5587820#5587820)  [参见](https://stackoverflow.com/questions/5115637/evenly-distributed-height-of-child-elements-with-css)  [参见](https://stackoverflow.com/questions/9080633/can-a-css-pixel-be-a-fraction)

如果非要显示这种“极细的”东西，据说可以用 `transform: scale()` 去做。

据说在 Retina 显示屏上也有类似问题，待考。