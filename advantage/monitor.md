# 进程内监控
前面介绍了toolbox模块，beego默认已经在进程开启的时候监控端口，但是默认是监听在`127.0.0.1:8088`,这样无法通过外网访问，当然你可以通过各种方法访问，例如nginx代理。

>>>为了安全，建议用户在防火墙把8088端口给屏蔽了。

默认监控是开放，你可以通过设置参数配置关闭监控：

	beego.EnableAdmin = false
	
而且你还可以修改监听的地址和端口：

	beego.AdminHttpAddr = "localhost"
	beego.AdminHttpPort = 8888
	
打开浏览器，输入URL：`http://localhost:8088/`，你会看到一句欢迎词：`Welcome to Admin Dashboard`。

目前由于刚做出来第一版本，因此还需要后续继续界面的开发。
	
## 请求统计信息
访问统计的url地址`http://localhost:8088/qps`，展现如下所示：

	| requestUrl                                        | method     | times            | used             | max used         | min used         | avg used         |
	| /                                                 | GET        |  2               | 2.35ms           | 1.30ms           | 1.04ms           | 1.17ms           |
	| /favicon.ico                                      | GET        |  1               | 79.30us          | 79.30us          | 79.30us          | 79.30us          |
	| /src/xx                                           | GET        |  1               | 923.09us         | 923.09us         | 923.09us         | 923.09us         |
	| /src                                              | GET        |  1               | 792.93us         | 792.93us         | 792.93us         | 792.93us         |
	| /123                                              | GET        |  1               | 906.04us         | 906.04us         | 906.04us         | 906.04us         |

## 性能调试
性能监控包含多个命令，请求地址`http://localhost:8088/prof`

当你输入的时候会提示你如何进行详细的调试，显示如下界面：

	request url like '/prof?command=lookup goroutine'
	the command have below types:
	1. lookup goroutine
	2. lookup heap
	3. lookup threadcreate
	4. lookup block
	5. start cpuprof
	6. stop cpuprof
	7. get memprof
	8. gc summary

用户可以通过传递不同的command值获取不同的性能调试信息，比较常用的有`lookup goroutine`、`lookup heap`和`gc summary`

## 健康检查
需要手工注册相应的健康检查逻辑，才能通过URL`http://localhost:8088/healthcheck`获取当前执行的健康检查的状态。

## 定时任务
用户需要在应用中添加了task，才能执行相应的任务检查和手工触发任务。

- 检查任务状态URL：`http://localhost:8088/task`
- 手工执行任务URL：`http://localhost:8088/runtask?taskname=任务名`
