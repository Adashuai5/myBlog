---
title: windows 7与 linux 双系统安装（免U盘）
date: 2018-06-03 22:30:14
tags: linux
---

之前一直看到 linux 系统的安利，决定在原 windows 7 系统下装个 linux 系统来学习。网上找了大量教程，遇到了各种各样的问题，花费了很长时间，终于成功。由于身边没有 U 盘，选择了免 U 盘安装的便捷方法。本次选择的 linux 系统版本为使用量最多的 ubuntu。下面分享安装的过程中的问题及解决方法。

**系统环境：**

windows 7（win10 相同）

**准备工具：**

1.EasyBCD，一款用来配置与调整启动配置数据的软件，本次我使用的是 2.3 版本。

2.Ubuntu 系统，[官网下载](https://link.zhihu.com/?target=https%3A//cn.ubuntu.com/download/)，选择自己喜欢的版本，本次我选用的是 Ubuntu 17.04 版本。

**windows 分区：**

从 windows 系统磁盘中分出 40-100G 空间作为 linux 系统存储空间

1.桌面右键我的电脑，点击管理->磁盘管理

![](https://upload-images.jianshu.io/upload_images/7094266-08c675192441c530.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.选择一个可用空间多的盘，右击选 压缩卷。压缩相应大小空间，本次我选用的是 80G，即 81920（可自行按实际情况选择 40-100G）

![](https://upload-images.jianshu.io/upload_images/7094266-1e878e73901c0b1b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.压缩完成后生成的盘为为分配，选择新建简单卷，一直点下一步就可以了。

![](https://upload-images.jianshu.io/upload_images/7094266-651995342bc7e591.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.若出现无法新建简单卷的情况，如下（未出现即分区成功，可直接看下一过程）

![](https://upload-images.jianshu.io/upload_images/7094266-45a5f96809ab9018.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

主分区和逻辑分区已满情况：磁盘主分区加上逻辑分区（绿色框区域）超过 4 个区，就会出现这种情况。（想了解可看[遇到此情况原因](https://link.zhihu.com/?target=https%3A//blog.csdn.net/qiushisoftware/article/details/19337945)）

由于我原本的逻辑分区空间不足，我选择的办法是将某个主分区转换成逻辑分区，这样就相当于将磁盘转化到 3.的盘的状态，即主分区和逻辑分区不超过 4 个。用到的软件是 DiskGenius [下载地址](https://link.zhihu.com/?target=http%3A//www.diskgenius.cn/download.php)

选中原来想分区的主分区盘 右击->转化为逻辑分区即可

![](https://upload-images.jianshu.io/upload_images/7094266-09adb29a2c6cc10d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后重复步骤 3 就能成功

**Ubuntu：**

将下载好的 Ubuntu iOS 镜像文件放到电脑某个盘根目录下，本次我选择的是 F 盘，然后解压到当前目录下（选个文件少的盘，安装完成后这些解压文件和镜像都没用了，文件多的话删除的时候比较蛋疼，好在解压下来的文件一般有相同的修改日期，可作为删除参考依据）。保证解压后的这些文件和 Ubuntu iOS 镜像文件在同一个盘的根目录下，要不然安装过程中可能出现找不到系统文件的情况。

![](https://upload-images.jianshu.io/upload_images/7094266-0d9f66878975eea7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/7094266-8f38604e93644e1e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**EasyBCD：**

打开 EasyBCD，选择添加新条目。在下半部分框里点击 ISO 项，名称随便填，路径选择你的 ubuntu ISO 镜像所在的地方。模式从磁盘运行。选完后，添加条目

![](https://upload-images.jianshu.io/upload_images/7094266-fc7fd3391c25169b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后点击编辑引导菜单，就可以看到刚才添加的条目了。选择倒计时，如果 Use Metro bootloader 没有勾选上，勾选下。完成后保存设置。

![](https://upload-images.jianshu.io/upload_images/7094266-16069c81c35d9de9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**进入 Ubuntu 安装：**

主要安装过程我参考了[\_牙牙](https://link.zhihu.com/?target=https%3A//www.jianshu.com/u/563525e5cc40)的简书  [地址](https://link.zhihu.com/?target=https%3A//www.jianshu.com/p/417c1001a559)  所给方法进行（由于图片无法截取，只能贴其博客了，大家可以按其博客从“4.关机重启，会出现两个选项，选 Ubuntu iOS，单击进入安装引导过程“开始）

当我进行到这一步时候

![](https://upload-images.jianshu.io/upload_images/7094266-fc2b00988be311dd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

出现了“因为不能卸载以下挂载点上分区：/cdrom”的提示框（找不到图了，遇到应该会懂）此时不要点继续（我点了继续然后安装了一晚上没动静），点后退。

解决方法是在此界面时选择试用 Ubuntu

![](https://upload-images.jianshu.io/upload_images/7094266-7e0728cbb8a2de16.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入后按快捷键 ctrl+alt+T 进入终端

输入 sudo umount -l /cdrom 回车即可继续进行安装 Ubuntu（‘-l’中‘l’是小写的 L）

若还是未安装成功，多尝试几遍，有与上述不一致的问题多 google，每个电脑情况不同，但是遇到问题基本上前人都解决过了，一定能有效解决。（ **Ctrl+Alt+Del**可以立即终结电脑的异常状态，因此安装未成功可用此快捷键快速重启）

相信你一定能愉快得开始玩耍 linux 系统的。

本文主要用于个人学习使用，如有侵权请联系我删除。

**主要参考博客：**

[win10 下装 ubuntu 双系统（免 U 盘）](https://link.zhihu.com/?target=https%3A//www.jianshu.com/p/417c1001a559)

其他参考链接已在文中注明。
