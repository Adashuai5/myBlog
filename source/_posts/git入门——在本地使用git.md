---
title: git 入门——在本地使用 git
date: 2018-06-05 21:05:27
tags: git
---

# 什么是 git

git 是世界上最好的分布式版本控制系统

什么意思？可以看廖雪峰的[git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)前面部分了解其概念

# 如何在本地使用 git

首先，打开你的命令行，本次我使用的是 Windows 上的 git bash，进入你的桌面 cd Desktop/

![](https://upload-images.jianshu.io/upload_images/7094266-43b9dc80ef559196.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在桌面创建一个文件夹，如 git-demo-1

mkdir git-demo-1

![](https://upload-images.jianshu.io/upload_images/7094266-0dc68b973297288f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**1\. git init 初始化本地仓库 .git**

进入这个目录：cd git-demo-1

然后输入命令：git init

这句命令会在 git-demo-1 里创建一个 .git 目录

可以用 ls -la 观察这个目录

![](https://upload-images.jianshu.io/upload_images/7094266-234bac65ee856269.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2\. git status -sb 观察当前文件状态**

在 git-demo-1 目录里创建一个文件如 index.html

touch index.html

运行  git status -sb  可以看到文件前面有 ??

![](https://upload-images.jianshu.io/upload_images/7094266-5e3a74ba0f7d5209.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**3\. git add 文件名或 git add.**

?? 表示 git 不知道如何对待这个新的文件

此时要用 git add 将文件添加到「暂存区」

git add index.html（若文件较多，一个个加麻烦，可直接用 git add. 一次性将所有变动加到暂存区）

然后可以再 git status -sb 观察其状态

![](https://upload-images.jianshu.io/upload_images/7094266-aae00cd046749ce5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

?? 变成了 A 即告诉 git 这些文件我要加到仓库里

**4. git commit -m "信息" 将文件正式提交到本地仓库（.git）**

同样你可以一个个提交文件

git commit index.html -m '添加 index.html'

或者一次提交所有文件

git commit . -m "添加了几个文件"

再运行  git status -sb

![](https://upload-images.jianshu.io/upload_images/7094266-0dc17938fa6c7440.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

出现## master 说明你已经将文件上传成功了

这时你可以用  git log 看历史变动

![](https://upload-images.jianshu.io/upload_images/7094266-497d1b90a4b1e1cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

至此，一次在本地使用 git 的过程就完成了

如果对已有文件有新的变动，我们只需要依次执行 git add xxx 和 git commit -m 'xxx' 两个命令即可

---

# 总结一下就是

**1\. git init 初始化本地仓库 .git**

**2\. git add 文件名或 git add.**

**3. git commit -m "信息" 将文件正式提交到本地仓库（.git）**

**有新的变动， git add xxx 和 git commit -m 'xxx'**

**过程中用  git status -sb 观察当前文件状态**

**最后可用  git log 看历史变动**

---

本文主要用于个人学习使用，如有侵权请联系我删除。

一些参考：

[git 教程](http://www.runoob.com/git/git-tutorial.html)

[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

[廖大大-git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
