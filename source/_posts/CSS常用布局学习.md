---
title: CSS 常用布局学习
date: 2018-06-22 22:35:31
tags: CSS
---

最近开始学习 CSS，了解了一些基础和常规写法。CSS 的知识十分复杂，是值得不断发掘和完善的一个前端模块。对于新人来说，最好的方法就是尝试，去模仿，遇到问题再去深入，一点一点得增加对 CSS 的基础的理解。

CSS 布局对于新人来说，是一个比较基础的难点，首先我们应该理解一些常用的布局属性

[学习 CSS 布局](http://zh.learnlayout.com/)  通过这以网站，学习**'display'**，**'position'**  以及  **'float' **等属性，加深对其认识。

![](https://upload-images.jianshu.io/upload_images/7094266-da5183cded1d63d5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

下面介绍几种常用的布局方法

# 1.左右布局

1.1.用  **'float' **实现左右布局

![](https://upload-images.jianshu.io/upload_images/7094266-36b825766bb976e4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

只要设定两个布局块的宽度总和为 '**container'(容器) **的宽，那么俩个 class 的 float 属性可均为  **'float:left;' **

也可以用以下方法让右边块级元素自适应左边达到左右布局

![](https://upload-images.jianshu.io/upload_images/7094266-95e2ada432bbbcee.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

即给  **'right'**  的宽度加上  **'margin-left'**

1.2.用** 'position' **实现左右布局

![](https://upload-images.jianshu.io/upload_images/7094266-5711c22ce85c4def.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

父元素设置为**position:relative;**

left 设置固定宽度，设定为**绝对定位'position:absolute'**。

right 设置为**相对定位'position:relative'**。

right 设置左边距，**'margin-left' **为左侧栏的宽度。

# 2.左中右布局

2.1.用  **'float' **实现左右布局

![](https://upload-images.jianshu.io/upload_images/7094266-4af2cbc2a81b81ff.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其原理与  **'float' **左右布局一样，且也可以用自适应。

值得注意的是  **'middle' **所在块与  **'left' **所在块一样，要用  **'float:left;' **

而  **'right'**  所在块可以用  **'float:left'**  或  **'float:right;'**  以及自适应。

2.2.用** 'position' **实现左中右布局

![](https://upload-images.jianshu.io/upload_images/7094266-83bd3380ae9c53c6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

原理与前面类似，值得注意的是，我们要调整一下 html 的布局，保证  **'right' **列 div 在  **'middle' **列 div 前，不然会出现第三块换行显示的情况，此问题涉及**文档流**

**文档流：**文档内元素的流动方向：内联元素从左往右，宽度不够另起一行继续；块级元素，每一块占一行，从上到下依次往下

所以同理，2.1.中**'middle' **若用自适应，也要调整 html 与上面一样

# 3.水平居中

其实前面已经用到了水平居中的方法

**margin: 0 auto;**  常用于块级元素

![](https://upload-images.jianshu.io/upload_images/7094266-467bc19891cc934f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当然还有其他水平居中及垂直居中的方法，网上有很多相关博客。如[16 种方法实现水平居中垂直居中](http://louiszhai.github.io/2016/03/12/css-center/)

---

另外，如何实现将垂直元素变成水平，也可以用**'float:left;'**

方法如下：

1.给所有的子元素加  **float:left**

![](https://upload-images.jianshu.io/upload_images/7094266-ef4aadee77723993.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.给父元素加  **clearfix 类  **（其目的是去掉**float:left **产生的 bug，一定会有 bug，因此一定要加上）

![](https://upload-images.jianshu.io/upload_images/7094266-d7be5e5d7ed3302e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**clearfix 类**写法如下

![](https://upload-images.jianshu.io/upload_images/7094266-0b746da3ed8fa6cb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

通过上述知识，相信你对**'display'**，**'position'**  以及  **'float'**  等属性已经有所认识。后续学习过程中了解了  **'flex'**属性（其实[学习 CSS 布局](https://link.zhihu.com/?target=http%3A//zh.learnlayout.com/toc.html)里提到了，有兴趣可以看 MDN 文档，但是看文档很多时候不能快速理解）推荐看看大佬们的博客，这里推荐阮一峰老师关于**'flex'布局**的[博客](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)，上述 1，2 种布局方式现已经不提倡，**'flex'**是个强大的属性，**'flex'布局**应作为布局的首选。

本文主要用于个人学习使用，如有侵权请联系我删除

主要参考：

[学习 CSS 布局](http://zh.learnlayout.com/toc.html)

[CSS 常见布局](https://leohxj.gitbooks.io/front-end-database/html-and-css-basic/css-layout.html)

[DIV + CSS 页面基本布局总结](https://www.jianshu.com/p/c6673f8a6a5a)

[16 种方法实现水平居中垂直居中](http://louiszhai.github.io/2016/03/12/css-center/)
