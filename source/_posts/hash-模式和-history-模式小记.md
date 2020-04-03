---
title: hash 模式和 history 模式小记
date: 2019-11-28 21:55:33
tags: 设计模式
---

# 前端路由

随着 ajax 的流行，异步数据请求体验极具提升，用户得以在不刷新浏览器的情况下进行页面交互，而异步交互体验的更高级版本就是 SPA —— 单页应用。单页应用不仅仅是在页面交互时无刷新，连页面跳转都是无刷新的，为了实现单页应用，所以就有了前端路由。

# 前端路由常用的两种模式

类似于服务端路由解析对应的 url 路径，返回对应的页面/资源的方式，前端路由实现起来其实也很简单，就是匹配不同的 url 路径，进行解析，然后动态的渲染出区域 html 内容。
这样自然 url 每次变化的时候，都会造成页面的刷新。那么在改变 url 的情况下，如何保证页面的不刷新？

## hash 模式

在 2014 年之前，大家是通过 hash 来实现路由，url hash 就是类似于：

```html
http://www.xxx.com/#/login
```

这种 # 后面 hash 值的变化，并不会导致浏览器向服务器发出请求，浏览器不发出请求，也就不会刷新页面。另外每次 hash 值的变化，还会触发[`window.onhashchange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onhashchange)事件，通过这个事件我们就可以知道 hash 值发生了哪些变化。然后我们便可以监听 hashchange 来实现更新页面部分内容的操作：

```
function hashChanged() {
   if (location.hash === "#ada") {
        ada();
    }
}
window.addEventListener('hashchange', hashChanged)
```

### 为什么改变 hash 不刷新页面？——[URL 的井号‘#’](http://www.ruanyifeng.com/blog/2011/03/url_hash.html)

‘#’ 代表网页中的一个位置，它后面的字符，就是该位置的标识符，它只对浏览器有用，服务器不识别，因此 HTTP 请求不会包含 # (想要请求 url 包含 # ，可使用 [encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)
进行部分转义)

`改变 hash ，只会让浏览器滚动到相应位置，不会重载网页`

## history 模式

2014 年后，HTML5 引入了  [history.pushState()](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)  和  [history.replaceState()](<https://developer.mozilla.org/en-US/docs/Web/API/History_API#The_replaceState()_method>)  方法，它们分别可以添加和修改历史记录条目，通过这两个 API 可以改变 url 地址而无须重新加载页面。
同时还有[`window.onpopstate`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onpopstate "window.onpopstate是popstate事件在window对象上的事件处理程序.")事件：
在浏览器点击后退、前进按钮(或者在 JavaScript 中调用 history.back()、history.forward()、history.go() 方法) 可以触发 popstate 事件

```
function stateChange() {
   // 一些 history 方法调用
}
window.addEventListener('popstate', stateChange)
```

通过这些就能用另一种方式来实现前端路由了，但原理都是跟 hash 实现相同的。

用了 HTML5 的实现，单页路由的 url 就不会多出一个 #，变得更加美观。**但因为没有 # 号，所以当用户刷新页面之类的操作时，浏览器还是会给服务器发送请求。**为了避免出现这种情况，history 模式需要服务器的支持，把所有路由都重定向到根页面。

## hash 模式和 history 模式对比

1.  无 # 的 history 模式更自然
2.  history 模式需要 ie9 以上，相对于 hash 模式的 ie8 兼容性差
3.  history 模式需服务器端配合，反过来说 hash 模式不支持服务端渲染

## 控制 vue-router 内的自动降级

vue-router 默认 hash 模式，且在 history 模式下当浏览器不支持 history.pushState 时默认回退到 hash 模式
因此在 IE9 下的服务端渲染需要设置 fallback 为 false
