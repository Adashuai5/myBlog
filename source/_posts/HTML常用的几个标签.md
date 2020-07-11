---
title: HTML 常用的几个标签
date: 2018-06-13 22:04:49
tags: HTML
---

**遇到新的标签属性等不会用可以用 JS BIN 尝试看看效果，就知道了**

# 常见标签详解

## **1\. iframe** **标签**

**嵌套页面**

1.1. **iframe 标签**的 **frameborder**  属性

**iframe 标签**自带边界 border，所以用这个属性可以去边界，如图

![](https://upload-images.jianshu.io/upload_images/7094266-1031b6812b8aaf57.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/7094266-fa67255c8a244a71.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1.2.**iframe 标签**的  **src** 属性：主要用来加链接

1.3.**iframe 标签**的  **name** 属性

**name 属性**与** a 标签**一起使用有效，如图

![](https://upload-images.jianshu.io/upload_images/7094266-d6e908d8da74ea14.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## **2\. a 标签**

**跳转页面（HTTP GET 请求）**

**target 属性**

**target="\_blank \_top \_parent \_self"** 的区别，看意思就懂了分别是跳转 新空白页面；最首页（用于不止两个页面，跳到第一个页面）；父页面（不止两个页面，跳到当前页面父页面）；自身页面

命令行下载 http 服务工具

```
npm i -g http-server
```

这样就不用自己写服务了，然后用下面命令打开服务器

```
http-server -c -1
```

![](https://upload-images.jianshu.io/upload_images/7094266-23d055b34597b717.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

打开服务器

下面的路径都可以访问文件夹所在网页文件，复制其中一个在浏览器上访问即可

如http://10.216.155.182:8080

![](https://upload-images.jianshu.io/upload_images/7094266-5af1c1c11575c480.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

只有  **href="#"** 没有 **get** 请求

此外  **a 标签**  的 **href**  有以下几种方法

![](https://upload-images.jianshu.io/upload_images/7094266-787bd332399011ba.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3.form 标签

**跳转页面（HTTP POST 请求）**

3.1. **from 标签** 需要加 **（提交按钮）submit** 来显示跳转，如图

![](https://upload-images.jianshu.io/upload_images/7094266-aaa0d33e641cd112.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/7094266-e664c2791e3c60dc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.2. **from 标签**  主要用来发起 post 请求（如登录时输入账号密码时候）

![](https://upload-images.jianshu.io/upload_images/7094266-ca38a55f51850bee.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在网页中点击提交，Network 中 post 请求中的第四部分 From Data 如图

![](https://upload-images.jianshu.io/upload_images/7094266-22538ebbc2c5f43d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

若是 HTTP 协议，密码便是明文："222"，这就是为什么会有 HTTPS 出现

3.3. **from 标签**与**a 标签**一样也有** target**

## **4\. input 标签和 button 标签**

**input 要学的比较多，可以结合[MDN 文档](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)实例学习**

![](https://upload-images.jianshu.io/upload_images/7094266-fad8a6d86142a599.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**input type="button"**和 **button** 的区别

![](https://upload-images.jianshu.io/upload_images/7094266-583d5833841661dc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

区别是  **input** 是空元素，无法内联其他标签，而  **button** 显然可以

注：若 form 表单只有一个  **button 按钮**而无 **type** 属性，**button** 直接升级为  **submit**（跳转）

## 5.table 标签

较完整示例如图

![](https://upload-images.jianshu.io/upload_images/7094266-410da64f04c3a907.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1\. 很多人会忽略  **colgroup**  的使用，它可以用来给 table 的表列表加宽度等属性

2\. thead tbody tfoot 三个标签可以省略，加上的好处是给了每一部分定义，即使他们顺序打乱，浏览器也可以很好得形成原列表

3\. 上图中 table 的 border 有空隙可以用

**border-collapse**  来去掉

![](https://upload-images.jianshu.io/upload_images/7094266-b6ee3f969de3dc94.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

本文主要用于个人学习使用，如有侵权请联系我删除
