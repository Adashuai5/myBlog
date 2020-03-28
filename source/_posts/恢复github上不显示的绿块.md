---
title: 恢复 github 上不显示的绿块
date: 2018-07-16 00:50:39
tags: git
---

github 是一个良好的记录自己代码的 git 版本控制平台，看到自己有关的 contributions 的小绿块是件开心的事。但是如果，你的每次 commit 都没有相应的小绿块，是不是很伤感呢。

之前我的 github 一直存在这个问题，虽然写代码不是为了说有这个小绿块。但是没有的话，commit 的积极性会大受打击。

最后 google 终于找到了解决方法，原来我 github 绑定的是 qq 邮箱，而 git bash 上保存的 email 地址是谷歌邮箱。（其实之前也搜索到这些答案，但是由于确信当时使用的是谷歌邮箱而一直没有去看，当然或许是没想到。）

方法是在 github 的 settings 里 Emails 中 Add 你一直错用的邮箱，这样小绿块就回来了，开心，以后又可以愉快得 commit 了

![](https://upload-images.jianshu.io/upload_images/7094266-4913eaff0e17eecc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注意只有你的终端里绑定的邮箱有效，上面的方法才可行，即你的小绿块记录会回来；如果你用的是无效邮箱，那就只能改终端绑定邮箱为 github 上邮箱来让未来的小绿块不丢失了（或许还有别的找回无效邮箱提交 commit 小绿块的方法，我不知道）有关教程可看我提供参考链接

---

本文主要用于个人学习使用，也希望能帮到你

参考：

[解决提交到 GitHub 首页不显示的问题](https://blog.csdn.net/Cloudox_/article/details/50284193)

[解决 github 提交 commit,contributions 不统计显示绿色的问题](https://www.cnblogs.com/dongliu/p/5782329.html)
