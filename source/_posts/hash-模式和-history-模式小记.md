---
title: 【前端路由】这可能是最容易理解的一篇了
date: 2020-4-4 16:45:33
tags: 设计模式
---

随着 ajax 的流行，异步数据请求体验极具提升，用户得以在不刷新浏览器的情况下进行页面交互，而异步交互体验的更高级版本就是 SPA —— 单页应用。

单页应用不仅仅是在页面交互时无刷新，连页面跳转都是无刷新的，为了实现单页应用，就有了**前端路由**。

# 常用的两种模式

类似于服务端路由解析对应的 url 路径，返回对应的页面/资源的方式，前端路由实现起来其实也很简单，就是匹配不同的 url 路径，进行解析，然后动态的渲染出区域 html 内容。

这样自然 url 每次变化的时候，都会造成页面的刷新。

那么在改变 url 的情况下，如何保证页面的不刷新？

## hash 模式

在 2014 年之前，大家是通过 hash 来实现路由，url hash 就是类似于：

```html
https://www.xxx.com/#/login
```

这种 # 后面 hash 值的变化，并不会导致浏览器向服务器发出请求，浏览器不发出请求，也就不会刷新页面。

### 为什么改变 hash 不刷新页面？——[URL 的井号‘#’](http://www.ruanyifeng.com/blog/2011/03/url_hash.html)

> ‘#’ 代表网页中的一个位置，它后面的字符，就是该位置的标识符，它只对浏览器有用，服务器不识别，因此 HTTP 请求不会包含 #

(想要请求 url 包含 # ，可使用 [encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)
进行部分转义)

**改变 hash ，只会让浏览器滚动到相应位置，不会重载网页**

每次 hash 值的变化，会触发 hashchange 事件，通过[`window.onhashchange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onhashchange)监听该事件我们就可以检测变化的 hash 值来做相应的页面操作。

### 简易实现

接下来我们用最简单的代码实现 hash 模式，仅为了解其思想（你可以直接复制到一个 html 上并通过静态服务器如 [http-server](https://www.npmjs.com/package/http-server) 查看）：

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Hash 路由</title>
  </head>
  <body>
    <ul>
      <li><a href="#red">红色背景</a></li>
      <li><a href="#green">绿色背景</a></li>
      <li><a href="#grey">灰色背景</a></li>
    </ul>
    <script>
      function watchHash() {
        const hash = window.location.hash.slice(1) || '/';
        switch (hash) {
          case "red":
            document.body.style.background = "red";
            break;
          case "green":
            document.body.style.background = "green";
            break;
          case "grey":
            document.body.style.background = "grey";
            break;
        }
      }
      window.addEventListener("hashchange", watchHash, false);
      window.addEventListener("load", watchHash, false);
    </script>
  </body>
</html>
```

#### 如何实现最基础的前进后退？

这里我们简单实现一下后退功能，前进思路类似：

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Hash 路由</title>
  </head>
  <body>
    <ul>
      <li><a href="#red">红色背景</a></li>
      <li><a href="#green">绿色背景</a></li>
      <li><a href="#grey">灰色背景</a></li>
    </ul>
    <button id="back" disabled="true">后退</button>
    <script>
      var isGoBack = false;
      const history = [];
      function watchHash() {
        const hash = window.location.hash.slice(1) || "/";
        // 防止后退时也记录 hash
        if (!isGoBack && window.location.hash) {
          history.push(window.location.hash);
        }
        back.disabled = history.length > 0 ? false : true;
        console.log(history);
        switch (hash) {
          case "red":
            document.body.style.background = "red";
            break;
          case "green":
            document.body.style.background = "green";
            break;
          case "grey":
            document.body.style.background = "grey";
            break;
          default:
            document.body.style.background = "#fff";
        }
        isGoBack = false;
      }
      back.onclick = goBack;
      function goBack() {
        isGoBack = true;
        if (history.length > 0) {
          history.pop(1);
          window.location.hash = history[history.length - 1] || "";
        } else {
          back.disabled = true;
        }
      }
      window.addEventListener("load", watchHash, false);
      window.addEventListener("hashchange", watchHash, false);
    </script>
  </body>
</html>
```

思路就是通过一个数组记录每次 hashchange 事件的 hash 值，点击后退时取出上一次 hash 值覆盖当前页面的 hash。

需要注意的是需要区别当前 hash 是后退生成（后退时的 hash 变化不应记录）的还是跳转生成，避免重复记录。

![](https://upload-images.jianshu.io/upload_images/7094266-a0a5b8004805e7da.gif?imageMogr2/auto-orient/strip)

## history 模式

可以看到，在早期 hash 模式虽然可以实现前端路由，但其后退前进操作就十分麻烦。

2014 年后，HTML5 引入了 [History](https://developer.mozilla.org/zh-CN/docs/Web/API/History) API，让我们能够快速访问页面历史。

其中  [history.pushState()](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)  和  [history.replaceState()](https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState) 方法，它们分别可以添加和修改历史记录条目，通过这两个 API 可以改变 url 地址而无须重新加载页面。

同时还有 popstate 事件：
通过[`window.onpopstate`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onpopstate "window.onpopstate是popstate事件在window对象上的事件处理程序.")可以监听在**浏览器点击后退、前进按钮(或者在 JavaScript 中调用 history.back()、history.forward()、history.go() 方法)** 触发的 popstate 事件。

通过这些就能用另一种方式来实现前端路由了，但原理都是跟 hash 实现相同的。

### 用 history 实现上面 hash 代码

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>History 路由</title>
  </head>
  <body>
    <ul id="ul">
      <li><a href="/red">红色背景</a></li>
      <li><a href="/green">绿色背景</a></li>
      <li><a href="/grey">灰色背景</a></li>
    </ul>
    <script>
      const path = window.location.pathname;
      history.replaceState({ path: path }, null, path);
      ul.addEventListener("click", (e) => {
        if (e.target.tagName === "A") {
          e.preventDefault();
          const path = e.target.getAttribute("href");
          history.pushState({ path: path }, null, path);
          watchHistory(path);
        }
      });
      function watchHistory() {
        const path = window.location.pathname;
        switch (path) {
          case "/red":
            document.body.style.background = "red";
            break;
          case "/green":
            document.body.style.background = "green";
            break;
          case "/grey":
            document.body.style.background = "grey";
            break;
          default:
            document.body.style.background = "#fff";
        }
      }
      window.addEventListener("popstate", watchHistory, false);
    </script>
  </body>
</html>
```

用了 HTML5 的实现，单页路由的 url 就不会多出一个 #，变得更加美观。

**但因为没有 # 号，所以当用户刷新页面之类的操作时，浏览器还是会给服务器发送请求。**

为了避免出现这种情况，history 模式需要服务器的支持，把所有路由都重定向到根页面。

### 如何监听 pushState 和 replaceState 的变化

经过理论及实践我们知道 replaceState()，pushState() 两个 API 不会触发 popstate 监听事件。

我们可以生成全新的 window 监听事件监听其变化：

```
function addListen(type) {
  const source = history[type];
  return function () {
    const event = new Event(type);
    event.arguments = arguments;
    window.dispatchEvent(event);
    return source.apply(this, arguments);
  };
}

history.pushState = addListen("pushState");
history.replaceState = addListen("replaceState");

window.addEventListener("replaceState", (e) => {
  console.log("我监听了 replaceState");
});
window.addEventListener("pushState", (e) => {
  console.log("我监听了 pushState");
});
```

# 两种模式对比

1.  无 # 的 history 模式更自然
2.  history 模式需要 IE9 以上，相对于 hash 模式的 IE8 兼容性差
3.  history 模式需服务器端配合，反过来说 hash 模式不支持服务端渲染

# 结语

以上就是前端路由的 hash 和 history 两种模式的主要原理及实现思路了，如果你觉得不错，别忘了点个赞 😄！

---

本文参考：

[面试官: 你了解前端路由吗?](https://juejin.im/post/5ac61da66fb9a028c71eae1b)

[阿里 P7：你了解路由吗？](https://juejin.im/post/5e85cb8151882573c66cf63f)

[[实践系列]前端路由](https://github.com/webfansplz/article/issues/1)
