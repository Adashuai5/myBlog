---
title: JavaScript 原型和原型链
date: 2018-07-12 00:51:42
tags: JavaScript
---

JavaScript 中除了基础类型外的数据类型，都是对象（引用类型）。但是由于其没有 类（class，ES6 引入了 class，但其只是语法糖）的概念，如何将所有对象联系起来就成立一个问题，于是就有了原型和原型链的概念。

---

> 每个实例对象（ object ）都有一个私有属性（称之为 **proto** ）指向它的构造函数的原型对象（prototype ）。该原型对象也有一个自己的原型对象( **proto** ) ，层层向上直到一个对象的原型对象为 null。根据定义，null 没有原型，并作为这个原型链中的最后一个环节。

![](https://upload-images.jianshu.io/upload_images/7094266-c9e28000b43ca445.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面是 [MDN 里有关原型链知识](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) 的摘录，什么意思？让我们来解释一下

事实上 JavaScript 所有数据都可以以对象的形式表现：由于函数是对象，我们可以用构造函数的方法使得 Number、Boolean、String 变成对象。

下面以 Number 为例 （其他类型也一样）

可以用 var 基本类型 = new 对应基本类型的函数() 的方法创建一个新函数

var n = new Number() 创建一个 Number 函数，其是一个对象

![](https://upload-images.jianshu.io/upload_images/7094266-62536de6cd21ab12.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里的 n 就是 Number 的实例对象，可以看到 n 里面有一个 **proto** 指向 Number 所指向的原型对象（也是 n 自己本身的原型对象），Number 为 n 的构造函数，它通过 prototype 指向自己的原型对象，而后又可以通过 constructor 指向回 Number 本身；

而 Number 函数也有一个 **proto** 指向 Object 这个构造函数的原型对象，Object 通过 prototype 指向自己原型对象 ；

Object 函数没有 **proto**，证明其已经到达最后的属性层，他的 **proto** 指向为 null。

即

![](https://upload-images.jianshu.io/upload_images/7094266-fc991a402727ca56.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**以上一整个原型与原型层层相链接的过程即为原型链**

其可以将公用属性存放在同一原型层中，实现继承、节省内存空间等。

> 当您访问实例的属性时，JavaScript 首先会检查它们是否直接存在于该对象上，如果不存在，则会 [[Prototype]] 中查找。这意味着你在 prototype 中定义的所有内容都可以由所有实例有效共享，你甚至可以稍后更改部分 prototype，并在所有现有实例中显示更改（如果需要）。

---

通过以上例子我们可以得到下面两个“公式”

**var 对象 = new 函数()**

**对象.**proto** === 对象的构造函数.prototype**

我们已经知道

**var n = new Number()**

**n.**proto** === Number.prototype //true**

那么  **Number.**proto\*\*\*\* ？

Number 的构造函数是 Function，即 Number 是 Function 的实例

即有  **Number.**proto** === Function.prototype**

那么同理

**var object = new Object()**

**object.**proto** === Object.prototype**

**Object.**proto** === Function.prototype**

再进一步推断

**var function = new Function()**

**function.**proto** === Function.prototype**

**Function.**proto** === Function.prototype**

![](https://upload-images.jianshu.io/upload_images/7094266-b6a6447f260e8db4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

本文主要用于个人学习使用，如有侵权请联系我删除。

参考及推荐：

[继承与原型链](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

[Javascript 继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

[白话原型和原型链](https://juejin.im/post/599d69fc6fb9a0248f4a7b31)

[JavaScript 深入之从原型到原型链 #2](https://github.com/mqyqingfeng/Blog/issues/2)

[饥人谷课件-原型链和继承](http://book.jirengu.com/fe/%E5%89%8D%E7%AB%AF%E8%BF%9B%E9%98%B6/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE.html)
