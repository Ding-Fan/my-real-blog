---
title: 尝试安装 Arch Linux
date: 2018-09-03 19:26:36
tags:
---

tl;dr: 最终我装了 Manjaro 。

Mac 越来越卡，时不时出现充不进电的现象，屏幕也偶尔花屏。是时候换一台装 Arch Linux 的笔记本了。

**首先**，阅读 Arch Wiki 里的 [Faq](https://wiki.archlinux.org/index.php/Frequently_asked_questions) 。读了一会儿些按捺不住激动的心情，就去下载了。按照[指示](https://wiki.archlinux.org/index.php/Category:Getting_and_installing_Arch)去[下载](https://www.archlinux.org/download/)了 `.iso` 文件和相应的 `.sig` 文件。然后到了 **Verify signature** 这一步，报错了。。。

```
gpg: Can't check signature: No public key
```

想去问又不好意思开口，于是动手开始搜索，不一会儿就[搜到了](https://bbs.archlinux.org/viewtopic.php?id=236213)。其中给出了[解决方案](http://wooledge.org/~greg/crypto/node41.html)。

```zsh
gpg --gen-key
```

结果我的 iTerm2 显示乱码了。。。大概是我用了中文名？不清楚。关掉重开一个 Tab 。

这次使用了英文名，到了这一步又报错了

```
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.

gpg: agent_genkey failed: Timeout
Key generation failed: Timeout
```

是不是因为我等着它去 generate 导致的？再试一次，我放首歌，看会儿[解决方案](http://wooledge.org/~greg/crypto/node41.html)。

结果失败了。报同样的错误。不知道是不是该用 `sudo` ？搜搜看先。

用 `gpg --version` 确定了版本是 `gpg (GnuPG) 2.2.1`

竟然搜到一个在 CSDN 上的答案，`$ rm -rf ~/.gnupg` 感觉好暴力。试试先。

然后又出现乱码。我打算用自带的 Terminal 再试一次。

仍然出现乱码。看来之前 `gpg: agent_genkey failed: Timeout` 的错误是由于第一次出现乱码强行关闭导致的。那么我们来搜索乱码的问题。

排查了 iTerm2 的字体问题，用了 powerline patched 字体。现在打算试试换一个 zsh 的 theme 。。。

换了一个 theme ，还是出现乱码。顺便查了查乱码用英文说叫做 weird characters 。

用 homebrew 更新了下 gpg ，还是出现乱码。打算睡了，明天问群。

到处都没问到结果，也没有查到。感觉很沮丧。于是装了个图形化界面工具（https://gpgtools.org/），给自己生成了 pubic key ，再次执行校验，就好了。

但是不知道接下来怎么校验。。。先继续吧。

```
dd if=path/to/arch.iso of=/dev/rdiskX bs=1M
```

进行这一步时报错 `dd: bs: illegal numeric value`

搜索得知，在 macOS 上要用 `bs=1m` 。参考[这里](https://rendezvouswithpavan.wordpress.com/2015/06/16/dd-bs-illegal-numeric-value-error-on-mac-os-x/)。

---

经过很长一段时间，仍然没有安装上 Arch Linux 。期间跟随一些其它教程安装，发现教程过期已经不能完全照搬了。通过几次失败安装和群里大家的建议，我明白还是得跟着 Wiki 走，教程起参考作用（比如 `wifi-menu` 在 Wiki 里没有提到）。是现在我卡在了 UEFI 和 bootloader 上。

趁着国庆放假再次发起挑战，竟然成功安装，开机进入 Arch Linux 的 Terminal 界面，百感交集。结果联网时发现没有 dialog 无法使用 wifi-menu 。整个人瘫倒在床上，我是谁？我在那儿？我这大半个假期都在做什么？拿起手机发了一条：我崩溃了，放弃。然后一会儿的功夫装上了 Manjaro 。
