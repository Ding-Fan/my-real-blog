---
title: wepy 中处理微信小程序的登录状态
date: 2018-08-21 17:12:42
tags:
---
基本流程是这样的：

**授权登录页**

1. 在 `onShow` 处调用 `wx.login()` 获取 `js_code`

2. 用户点击 `button` ，获取相关密文等，例如：

```html
  <button open-type="getUserInfo" @getuserinfo="onGotUserInfo">
    <view class="allow">
      允许
    </view>
  </button>
```

3. 调用后端提供的接口进行解密，拿到后端返回的 `token` ，存入 `storage`

**app.wpy**

1. 在 `interceptor` 中，在 `config` 里，从 `storage` 里取出 `token` 塞进 `header`

2. 在 `success` 里，判断 `statusCode` ，如果是 `401` 或 `412` 就 `reLaunch` 到授权登录页