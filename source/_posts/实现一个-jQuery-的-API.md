---
title: 实现一个 jQuery 的 API
date: 2018-07-29 00:01:59
tags: JavaScript
---

最近开始学习 jQuery，jQuery 是 JavaScript  最受欢迎的一个库，它让原本极不方便的 JS DOM API 变得十分易用，那么它是如何做到的呢？
要理解 jQuery 原理，我们可以用现有的 DOM 知识尝试写一个类似 jQuery 的 API

**首先我们写一个列表，给它加上 id**

![](https://upload-images.jianshu.io/upload_images/7094266-a1b5fa2c18276641.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**以选项 3 为节点，找到其兄弟节点（代码见截图）**

通过  **var allChildren = item3.parentNode.children**获取 **item3** 父节点的所以子节点，然后遍历所有子节点，选出不是 **item3** 的所有节点，这样就找到选项 3 的所以兄弟节点啦。可以 console.log 一下

（由于 array 是伪数组，不能用 push 的方法，所以我们用到  **array[array.length] = allChildren[i]**的方法）

![](https://upload-images.jianshu.io/upload_images/7094266-4e2f54c2e513b5ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后我们把这些代码**封装**一下（给个函数）

封装的好处有很多：给代码一个名字方便调用；**形成局部变量可以避免覆盖 JS 原始变量（立即调用函数）**等

给这个函数取个名字，如 getSiblings；把 item3 换成 node，这样输入任意节点都可以使用这个函数了；注意不要忘记 return

![](https://upload-images.jianshu.io/upload_images/7094266-ea2f6d7eaf37ac1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样我们就得到了一个函数  **function getSiblings(node){}**

---

现在你已经学会如何封装一个函数，让我们尝试封装函数：**function addClass(node, classes){}**

现在我们要给 item3 加 class 属性

首先我们声明一个 classes 对象，里面有 a、b、c 三个属性；**同时分别给它们一个布尔值，方便 add 和 remove**；遍历各个属性。

可以看到，class b、c 已经被添加到 item3 中了

![](https://upload-images.jianshu.io/upload_images/7094266-ab48d3fb806dae12.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

同样我们来封装一下这些代码

![](https://upload-images.jianshu.io/upload_images/7094266-8fa1e7aee94ca4f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

现在，只要你给一个 node 和 classes 于此函数，就可以给 该节点添加 classes 所包含的正确属性

# **命名空间：**

**给封装的函数一个名字，方便其他人使用，同时防止与前人命名的冲突。**

```
var Adadom = {}
Adadom.getSiblings(node)
Adadom.addClass(node, {a: false, b: true,c:true})
```

得到代码如下，这样做也能**避免将 JS 提供的 DOM 覆盖**

![](https://upload-images.jianshu.io/upload_images/7094266-a8a36cf56f38cbee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 能不能把 node 放在前面

```
node.getSiblings()
node.addClass()
```

方法一：扩展 Node 接口

直接在 Node.prototype 上加函数

Node 如何取到 item3？用 this ，why？把上面写成 .call 的形式，因为  **this 是 call 的第一个参数。**那么用 this 就显而易见了

![](https://upload-images.jianshu.io/upload_images/7094266-50bd8de7275ed2b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

但是这样太乱了，总不能所有人都在 Node 原型上加属性吧？所以有了方法 2

方法二：新的接口 BetterNode

示例如下

```
function Node2(node){
    return {
        element: node,
        getSiblings: function(){
       },
      addClass: function(){
    }
  }
}
let node =document.getElementById('x')
let node2 = Node2(node)
node2.getSiblings()
node2.addClass()
```

![](https://upload-images.jianshu.io/upload_images/7094266-9eb49bb5f7b83c3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这种方法叫做「无侵入」即对 Node 无侵入

# 把 Node2 改成 jQuery 吧

```
function jQuery(node){
    return {
        element: node,
        getSiblings: function(){
        },
        addClass: function(){
        }
      }
}
let node =document.getElementById('x')
let node2 =jQuery(node)
node2.getSiblings()
node2.addClass()
```

# 再给个缩写吧:alias

**window.\$ = jQuery**

即  **var node2 = \$(node)**

但是为了防止记混 node2 到底有没有引入 jQuery

大家通常这样写

```
var $node2 = $(node)
```

至此，你已经知道 jQuery 是个什么了：它就是一个函数，是 JS 原始 DOM 的扩展，便于我们更好得使用 JS 写代码的加强版 DOM API。

完整代码见  [github](https://github.com/Adashuai5/jQuery-demo/tree/master/jQuery%20API)

---

本文主要用于个人学习使用
