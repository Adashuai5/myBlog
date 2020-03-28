---
title: 理解 HTTP
date: 2018-06-07 22:16:57
tags: HTTP
---

# **什么是 HTTP**

**HTTP（HyperText Transfer Protocol）**超文本传输协议  [维基百科](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE#%E5%8D%8F%E8%AE%AE%E6%A6%82%E8%BF%B0)

**HTTP 的作用就是指导浏览器和服务器如何进行沟通**

**Client （浏览器）→ HTTP（请求）→Server（80 端口）→HTTP 响应 →Client（浏览器）**

![HTTP请求与响应](https://upload-images.jianshu.io/upload_images/7094266-e2b8fabd058d2313.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

浏览器负责发起请求

服务器在 80 端口接收请求

服务器负责返回内容（响应）

浏览器负责下载响应内容

---

# **HTTP 请求**

![请求的格式](https://upload-images.jianshu.io/upload_images/7094266-3255f775c068ece3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

请求最多包含四部分（图中 1、2、3、4），最少包含三部分。（也就是说第四部分可以为空）

第三部分永远都是一个回车（\n）

[动词](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE#%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95)有 GET/POST/PUT/PATCH/DELETE/HEAD/OPTIONS 等

这里的路径包括「查询参数」，但不包括「锚点」

如果你没有写路径，那么路径默认为 /

第 2 部分中的 Content-Type 标注了第 4 部分的格式

# **用 Chrome 发请求**

打开 Network（F12）

![](https://upload-images.jianshu.io/upload_images/7094266-ac46ff3c447bfe4a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

地址栏输入网址，如 www.baidu.com

在 Network 点击，查看 request，点击「view source」

![](https://upload-images.jianshu.io/upload_images/7094266-a26b808214a7f891.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到请求的前三部分了

如果有请求的第四部分，那么在 FormData 或 Payload 里面可以看到

---

# **HTTP 响应**

请求了之后，应该都能得到一个响应，除非断网了，或者服务器宕机了

![响应的格式](https://upload-images.jianshu.io/upload_images/7094266-0a2a709c31b4f71e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

状态码是服务器对浏览器说的话

[1xx 消息](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#1xx%E6%B6%88%E6%81%AF)——请求已被服务器接收，继续处理

[2xx 成功](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#2xx%E6%88%90%E5%8A%9F)——请求已成功被服务器接收、理解、并接受

[3xx 重定向](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#3xx%E9%87%8D%E5%AE%9A%E5%90%91)——需要后续操作才能完成这一请求

[4xx 请求错误](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#4xx%E8%AF%B7%E6%B1%82%E9%94%99%E8%AF%AF)——请求含有词法错误或者无法被执行

[5xx 服务器错误](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#5xx%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%94%99%E8%AF%AF)——服务器在处理某个正确请求时发生错误

状态解释没什么用

第 2 部分中的 Content-Type 标注了第 4 部分的格式

第 2 部分中的 Content-Type 遵循 MIME 规范

# **用 Chrome 查看响应**

打开 Network

输入网址

选中第一个响应

查看 Response Headers，点击「view source」

![](https://upload-images.jianshu.io/upload_images/7094266-c1ef5f68fe12bac5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

你会看到响应的前两部分

查看 Response 或者 Preview，你会看到响应的第 4 部分

---

**也可以用命令行发请求并得到响应**

用到**curl**命令，具体可以命令行[释义](https://explainshell.com/)（命令行及命令行释义可以看我相关[blog](https://www.jianshu.com/p/dcf636cbe6af)）

如：**curl -s -v -H  -- "https://www.baidu.com"**

![](https://upload-images.jianshu.io/upload_images/7094266-fb73225d2f20d079.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**请求的内容为**

```
> GET / HTTP/1.1

> Host: www.baidu.com

> User-Agent: curl/7.59.0

> Accept: */*

>

**响应的内容为**

< HTTP/1.1 200 OK

< Accept-Ranges: bytes

< Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform

< Connection: Keep-Alive

< Content-Length: 2443

< Content-Type: text/html

< Date: Thu, 07 Jun 2018 13:54:43 GMT

< Etag: "58860411-98b"

< Last-Modified: Mon, 23 Jan 2017 13:24:33 GMT

< Pragma: no-cache

* Server bfe/1.0.8.18 is not blacklisted

< Server: bfe/1.0.8.18

< Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/

<
```

还有很多可以尝试的 **curl** 命令

可以参考 [链接](http://man.linuxde.net/curl)

---

本文主要用于个人学习使用，如有侵权请联系我删除。

一些参考：

[HTTP-维基百科](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)

[curl 命令](http://man.linuxde.net/curl)
