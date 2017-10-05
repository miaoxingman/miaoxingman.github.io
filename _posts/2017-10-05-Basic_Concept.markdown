## Application Service and Web Service

首先比较容易搞混乱的是Server和Service的却别，我们先来看Web Server和Application Server的区别.
### Web Server and Application Server
Web Server和Application Server之所以被单独划分出来，应该是因为历史的原因。在Browser以及Web发展的最初阶段，Web Server就是意味着利用HTTP协议传输静态的content以及图片，HTTP1.0更是可以理解为一个文件传输协议。随着浏览器和Web技术的发展，越来越多的动态技术被发展出来，因此需要一个专门的Application Server来处理这些动态请求。现在大部分的Application Server也同时实现了Web Server的功能.

Application Server和Web Server的概念不仅仅局限于Java中，在Python的Flask库中直接返回一个html的page或者js的脚本就可以理解为一个Web Server；当使用jinja2动态生成一个Page的时候就可以理解为一个Application Server。

在本文中只讨论Java中的Web Server和Application Server。

#### Web Server

Web Server 或者叫 HTTP Server ,主要用于操作Http请求，包括接受客户端的请求以及响应。它可以处理请求，也可以将请求转发至其他服务器。Web Server 一般用来处理诸如html和css等静态资源，当遇到动态资源(jsp)的时候，Web Server将请求转至Application Server去做处理。

常用的Web Server以及其市场占有率如下。

<a href="#">
    <img src="{{ site.baseurl }}/img/web_server_market_shared.png" alt="Web Server market share of active site">
</a>

#### Application Server

Java中常用的Application Server的市场占有率如下所以，要理解各种Application Server的区别要先从J2EE Server说起。

<a href="#">
    <img src="{{ site.baseurl }}/img/java_application_server.png" alt="Web Server market share of active site">
</a>

J2EE是java技术不断适应和促进企业级应用过程中的产物，是使用Java技术开发企业级应用的一种事实上的工业标准。它包含了许多的组件，主要可以简化并且规范应用系统的开发和部署，进而提高可移植性、安全性以及再用价值。J2EE将服务器端的开发划分为客户端组件、Web层组件、业务层组件和企业信息系统四层。

<a href="#">
    <img src="{{ site.baseurl }}/img/j2ee_layer.jpg" alt="Web Server market share of active site">
</a>

通常情况下，Java的Application Server非常难写，因为要考虑底层的socket实现、SSL等应用层的安全、、Event以及线程模型、状态管理等细节，因此J2EE将业务逻辑组织为可重用的组件，J2EE服务器以容器的形式为每一个组件提供了底层的服务，因此容器封装了底层的实现细节，所以我们可以专注于实现业务层和表现层的逻辑。

我们常见的**Apache Tomcat**, **Jetty**, **Jave System Web Server**是一个Java containers，











