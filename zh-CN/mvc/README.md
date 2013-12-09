# beego的MVC结构介绍
beego是一个典型的MVC框架，它的整个执行逻辑如下图所示：

![](./../images/detail.png)

通过文字来描述如下：

1. 在监听的端口接收数据，默认监听在8080端口
2. 用户请求到达8080端口之后进入beego的处理逻辑
3. 初始化Context对象，根据请求判断是否为WebSocket请求，如果是的话设置Input，同时判断请求的方法是否在标准请求方法中("get", "post", "put", "delete", "patch", "options", "head")，防止用户的恶意伪造请求攻击造成不必要的影响。
4. 执行BeforeRouter过滤器，当然在beego里面有开关设置，如果用户设置了过滤器，那么该开关打开，这样可以提高在没有开启过滤器的情况下提高执行效率。如果在执行过滤器过程中，responseWriter已经有数据输出了，那么就提前结束该请求，直接跳转到监控判断
5. 开始执行静态文件的处理，查看用户的请求URL是否和注册在静态文件处理StaticDir中的prefix是否匹配，如果匹配的话，采用http包中默认的ServeFile来处理静态文件。
6. 如果不是静态文件开始初始化session模块(如果开启session的话)，所以这个里面大家需要主要，如果你的BeforeRouter过滤器用到了session就会报错，你应该把加入到AfterStatic过滤器中。
7. 开始执行AfterStatic过滤器，如果在执行过滤器过程中，responseWriter已经有数据输出了，那么就提前结束该请求，直接跳转到监控判断。
8. 执行过过滤器之后，开始从固定的路由规则中查找和请求URL相匹配的对象，这个匹配是全匹配规则，即如果用户请求的URL是`/hello/world`，那么固定规则中`/hello`是不会匹配的，只有完全匹配才算匹配，如果匹配的话就进入逻辑执行，如果不匹配进入下一环节的正则匹配。
9. 正则匹配是进行正则的全匹配，这个正则是按照用户添加beego路由顺序来进行匹配的，也就是说，如果你在添加路由的时候你的顺序影响你的匹配。和固定匹配一样，如果匹配的话就进行逻辑执行，如果不匹配进入Auto匹配。
10. 如果用户注册了AutoRouter，那么会通过`controller/method`这样的方式去查找对应的Controller和他内置的方法，如果找到就开始执行逻辑，如果找不到就跳转到监控判断。
11. 如果找到Controller的话，那么就开始执行逻辑，首先执行BeforeExec过滤器，如果在执行过滤器过程中，responseWriter已经有数据输出了，那么就提前结束该请求，直接跳转到监控判断。
12. Controller开始执行Init函数，初始化基本的一些信息，这个函数一般都是beego.Controller的初始化，不建议用户继承的时候修改该函数。
13. 是否开启了XSRF，开启的话就调用Controller的XsrfToken，然后如果是POST请求就调用CheckXsrfCookie方法。
14. 继续执行Controller的Prepare函数，这个函数一般是预留给用户的，用来做Controller里面的一些参数初始化之类的工作。如果在初始化中responseWriter有输出，那么就直接进入Finish函数逻辑。
15. 如果没有输出的话，那么根据用户注册的方法执行相应的逻辑，如果用户没有注册，那么就调用http.Method对应的方法(Get/Post等)。执行相应的逻辑，例如数据读取，数据赋值，模板显示之类的，或者直接输出json或者xml。
16. 如果responseWriter没有输出，那么就调用Render函数进行模板输出。
17. 执行Controller的Finish函数，这个函数是预留给用户用来重写的，用于释放一些资源。释放在Init中初始化的信息数据。
18. 执行AfterExec过滤器，如果有输出的话就跳转到监控判断逻辑。
18. 执行Controller的Destructor，用于释放Init中初始化的一些数据。
19. 如果这一路执行下来都没有找到路由，那么会调用404显示找不到该页面。
20. 最后所有的逻辑都汇聚到了监控判断，如果用户开启了监控模块(默认是开启一个8088端口用于进程内监控)，这样就会把访问的请求链接扔给监控程序去记录当前访问的QPS，对应的链接访问的执行时间，请求链接等。

接下来就让我们开始进入beego的MVC核心第一步，路由设置：

- [路由设置](./router.md)
- [控制器函数](./controller.md)
- [xsrf过滤](./xsrf.md)
- [session控制](./session.md)
- [flash数据](./flash.md)
- [请求数据处理](./params.md)
- [多种格式数据输出](./jsonxml.md)
- [表单数据验证](./validation.md)
- [模板输出](./view.md)
- [模板函数](./template.md)
- [错误处理](./errors.md)
- [静态文件处理](./static.md)
- [参数配置](./config.md)
- [日志处理](./logs.md)
