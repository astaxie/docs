---
root: true
name: Beego intro
sort: 0
---

# What is Beego
Beego is a http framework for developing Go application rapidly. It can be used for developing API, Web app, backend services quickly. It is a RESTFul framework.  It is inspired by tornado, sinatra and flask and integrated some Go features such as interface, struct inheritcace.  

## The Architecture of Beego
Here is the architecture of Beego:


![](../images/architecture.png)

Beego is build upon 8 independent modules. It's loose coupling framework. Beego is designed for modular programming. You can still use all these modules without using Beego's http logic. You can use cache module to handle your cache, you can use logs module for logging and you can use config module for processing file in many format. So you can use all these modules not only in Beego but also in many other applications such as socket games. This is one of the reasons that Beego became popular. If you know Lego you should know all magnificent modles are build of many small pieces. In the philosophy of Beego these modules are small piece of building blocks and the magnificent model is Beego. We will tall about more about the modules later.

## The executing logic of Beego

Beego is based on these modules so what's its executing logic? Beego is
a typical MVC architecture. Here is its executing logic:

![](../images/flow.png)

## The project structure of Beego

Here is the folder of a typical Beego project:

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

We can see the M (models), V (views), C (controllers) folders. `main.go` is the starting file.

>You can use [bee to create a new project](../install/bee.md)
