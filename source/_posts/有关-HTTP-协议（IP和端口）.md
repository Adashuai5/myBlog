---
title: 有关 HTTP 协议（IP 和端口）
date: 2018-06-08 14:51:05
tags: HTTP
---

# 网络与 IP

HTTP 协议的底层其实是由 TCP 协议和 IP 协议（简称 TCP/IP）构建的

**TCP 传输控制协议（Transmission Control Protocol）**

**1.[TCP 和 UDP 的区别是什么](https://www.nowcoder.com/questionTerminal/63c8b45c91a544bd8febc1f1ff02e3b5?toCommentId=73766)**

简答：TCP 可靠、面向连接、相对 UDP 较慢（求速度）；UDP 不可靠，不面向连接、相对 TCP 较快（求安全）。

2.[TCP 的三次握手指的是什么](https://github.com/jawil/blog/issues/14)

![](https://upload-images.jianshu.io/upload_images/7094266-5c97dd6f5e872dc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

简答：每次建立连接前，客户端和服务端之前都要先进行三次对话才开始正式传输内容，三次对话大概是这样的：

1\. 客户端：我要连接你了，可以吗

2\. 服务端：嗯，我准备好了，连接我吧

3\. 客户端：那我连接你咯。

然后 开始后面步骤

---

**IP 网络协议（英语：Internet Protocol）**

![](https://upload-images.jianshu.io/upload_images/7094266-03aaae9c062d73d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

路由器没有「固定的外网 IP」

路由器给自己的内网  **IP（192.168.1.1）**

本地** IP：127.0.0.1 **表示设备自己

特殊的** IP：0.0.0.0 **不表示任何设备

# 端口

你想要访问一个设备（前提是你使用的是 TCP 或 UDP 协议。还记得吗，HTTP 就使用了 TCP），只指定 IP 是不够的，还**必须**指定 端口（Port）

**原则：一个端口对应一个服务**

要提供 HTTP 服务你最好使用 80 端口（能不能使用别的端口？可以，不过不建议你违反约定）

要提供 HTTPS 服务你最好使用 443 端口（能不能使用别的端口？可以，不过不建议你违反约定）

要提供 FTP 服务你最好使用 21 端口（能不能使用别的端口？可以，不过不建议你违反约定）

**如何知道用何端口？**

0 到 1023 号端口对应的服务 [维基百科](https://zh.wikipedia.org/wiki/TCP/UDP%E7%AB%AF%E5%8F%A3%E5%88%97%E8%A1%A8#0.E5.88.B01023.E5.8F.B7.E7.AB.AF.E5.8F.A3)

**一共由多少端口？**

每个机器一共有 65535（2 的 16 次方减 1）个端口（这是协议规定的）。不过这些端口的使用由一些规定

0 到 1023（2 的 10 次方减 1）号端口是留给系统使用的，你只有拥有了管理员权限后，才能使用这 1024 个端口。

其他端口可以给普通用户使用

如果一个端口正在提供服务，也就是被占用了，那么就不能再使用这个端口。除非你先停掉正在占用这个端口的服务。

**使用 HTTP 协议访问另一个 IP 时，比如同时提供 IP 和端口号，缺一不可**

**访问网站时候浏览器帮你加了默认端口号，因此你不需要加也可以访问**

---

本文主要用于个人学习使用，如有侵权请联系我删除。
