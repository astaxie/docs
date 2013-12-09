# What is Beego
Beego is a http framework for developing Go application rapidly. It can be used for
developing API, Web app, backend services quickly. It is a RESTFul framework.
It is inspired by tornado, sinatra and flask and integrated some Go features
such as interface, struct inheritcace.

beego是一个快速开发Go应用的http框架，他可以用来快速开发API、Web、后端服务等各种应用，是一个RESTFul的框架，主要设计灵感来源于tornado、sinatra、flask这三个框架，但是结合了Go本身的一些特性(interface、struct继承等)而设计的一个框架。

## The Architecture of Beego
## beego的架构
Here is the architecture of Beego:


![](images/architecture.png)

Beego is build upon 8 independent modules. It's loose coupling
framework. Beego is designed for modular programming. You can still use all
these modules without using Beego's http logic. You can use cache module
to handle your cache, you can use logs module for logging and you can
use config module for processing file in many format. So you can use all these modules not only in Beego but also in many other applications such as socket games. This is one of the reasons that Beego became popular. If you know Lego you should know all maginaficent modles are build of many small pieces. In the philospic :TODO of Beego these modules are small pieces :TODO and the model is Beego. We will tall about more about the modules later.

beego是基于八大独立的模块之上构建的，是一个高度解耦的框架。当初设计beego的时候就是考虑功能模块化，用户即使不适用beego的http逻辑，也是可以在使用这些独立模块，例如你可以使用cache模块来做你的缓存逻辑，使用日志模块来记录你的操作信息，使用config模块来解析你各种格式的文件，所以不仅仅在beego开发中，你的socket游戏开发中也是很有用的模块，这也是beego为什么受欢迎的一个原因。大家如果玩过乐高的话，应该知道很多高级的东西都是一块一块的积木搭建出来的，而设计beego的时候，这些模块就是积木，高级机器人就是beego。至于这些模块的功能以及如何使用会在后面的文档会逐一介绍。

## The executing logic of Beego
## beego的执行逻辑

Beego is based on these modules so what's its executing logic? Beego is
a typical MVC architecture. Here is its executing logic:

既然beego是基于这些模块构建的，那么他的执行逻辑是怎么样的呢？beego是一个典型的MVC架构，他的执行逻辑如下图所示：

![](images/flow.png)

## The project structure of Beego
## beego项目结构

Here is the folder of a typical Beego project:
一般的beego项目的目录如下所示：

```
├── conf
│   └── app.conf   
├── controllers
│   ├── admin
│   └── default.go
├── main.go
├── models
│   └── models.go
├── static
│   ├── css
│   ├── ico
│   ├── img
│   └── js
└── views
    ├── admin
    └── index.tpl
```

We can see the M (models), V (views), C (controllers) folders. `main.go`
is the enter :TODO file.
从上面的目录结构我们可以看出来M(models目录)、V(views目录)、C(controllers目录)的结构，`main.go`是入口文件。

>You can use [bee to create a new project]
>你可以通过[bee来新建项目](bee.md)
