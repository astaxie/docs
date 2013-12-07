# bee介绍
bee是一个为了快速开发beego项目而创建的项目，通过bee可以快速的创建项目，自动的热编译，开发测试以及开发完之后打包发布的一整套从创建、开发到部署的方案。

## bee安装
通过如下的方式可以正确的安装bee工具：

	go get github.com/beego/bee
	

## bee命令详解
我们在命令行输入`bee`，可以看到如下的信息：

```
Bee is a tool for managing beego framework.

Usage:

	bee command [arguments]

The commands are:

    new         create an application base on beego framework
    run         run the app which can hot compile
    pack        compress an beego project
    api         create an api application base on beego framework
    router      auto-generate routers for the app controllers
    test        test the app
    bale        packs non-Go files to Go source files	
```	
### new命令
`new`命令是新建一个web项目，我们在命令行下执行`bee new 项目名`就可以创建一个新的项目，但是注意该命令必须在gopath下执行，这样就会在gopath目录下生成如下目录结构的项目：

```
bee new myproject
[INFO] Creating application...
/gopath/src/myproject/
/gopath/src/myproject/conf/
/gopath/src/myproject/controllers/
/gopath/src/myproject/models/
/gopath/src/myproject/static/
/gopath/src/myproject/static/js/
/gopath/src/myproject/static/css/
/gopath/src/myproject/static/img/
/gopath/src/myproject/views/
/gopath/src/myproject/conf/app.conf
/gopath/src/myproject/controllers/default.go
/gopath/src/myproject/views/index.tpl
/gopath/src/myproject/main.go
13-11-25 09:50:39 [SUCC] New application successfully created!
```

```
myproject
├── conf
│   └── app.conf
├── controllers
│   └── default.go
├── main.go
├── models
├── static
│   ├── css
│   ├── img
│   └── js
└── views
    └── index.tpl

8 directories, 4 files
```
### run命令
我们在开发Go项目的时候最大的问题是经常需要自己手动去编译，`bee run`命令是监控beego的项目，通过inotify监控文件系统，这样只有我们在开发过程中，我们就可以实时的看到项目修改之后的效果：
```
bee run
13-11-25 09:53:04 [INFO] Uses 'myproject' as 'appname'
13-11-25 09:53:04 [INFO] Initializing watcher...
13-11-25 09:53:04 [TRAC] Directory(/gopath/src/myproject/controllers)
13-11-25 09:53:04 [TRAC] Directory(/gopath/src/myproject/models)
13-11-25 09:53:04 [TRAC] Directory(/gopath/src/myproject)
13-11-25 09:53:04 [INFO] Start building...
13-11-25 09:53:16 [SUCC] Build was successful
13-11-25 09:53:16 [INFO] Restarting myproject ...
13-11-25 09:53:16 [INFO] ./myproject is running...
```
我们打开浏览器就可以看到效果`http://localhost:8080/`:

![](images/beerun.png)

如果我们修改了Controller下面的default.go文件，我们就可以看到命令行输出：
```
13-11-25 10:11:20 [EVEN] "/gopath/src/myproject/controllers/default.go": DELETE|MODIFY
13-11-25 10:11:20 [INFO] Start building...
13-11-25 10:11:20 [SKIP] "/gopath/src/myproject/controllers/default.go": CREATE
13-11-25 10:11:23 [SKIP] "/gopath/src/myproject/controllers/default.go": MODIFY
13-11-25 10:11:23 [SUCC] Build was successful
13-11-25 10:11:23 [INFO] Restarting myproject ...
13-11-25 10:11:23 [INFO] ./myproject is running...
```
刷新浏览器我们看到新的修改内容已经输出。
### api命令
上面的`new`命令是用来新建Web项目，我自己大多数时候是采用beego来开发api应用，提供对外的API，那么这个`api`命令就是用来创建API应用的，执行命令之后如下所示：
```
bee api apiproject
create app folder: /gopath/src/apiproject
create conf: /gopath/src/apiproject/conf
create controllers: /gopath/src/apiproject/controllers
create models: /gopath/src/apiproject/models
create tests: /gopath/src/apiproject/tests
create conf app.conf: /gopath/src/apiproject/conf/app.conf
create controllers default.go: /gopath/src/apiproject/controllers/default.go
create tests default.go: /gopath/src/apiproject/tests/default_test.go
create models object.go: /gopath/src/apiproject/models/object.go
create main.go: /gopath/src/apiproject/main.go
```
这个项目的目录结构如下：

```
apiproject
├── conf
│   └── app.conf
├── controllers
│   └── default.go
├── main.go
├── models
│   └── object.go
└── tests
    └── default_test.go
```
从上面的目录我们可以看到和Web项目相比，少了static和views目录，多了一个test模块，用来做单元测试的。
### test命令
这是基于`go test`进行封装的一个命令，执行beego项目test目录下的测试用例：
```
bee test apiproject
13-11-25 10:46:57 [INFO] Initializing watcher...
13-11-25 10:46:57 [TRAC] Directory(/gopath/src/apiproject/controllers)
13-11-25 10:46:57 [TRAC] Directory(/gopath/src/apiproject/models)
13-11-25 10:46:57 [TRAC] Directory(/gopath/src/apiproject)
13-11-25 10:46:57 [INFO] Start building...
13-11-25 10:46:58 [SUCC] Build was successful
13-11-25 10:46:58 [INFO] Restarting apiproject ...
13-11-25 10:46:58 [INFO] ./apiproject is running...
13-11-25 10:46:58 [INFO] Start testing...
13-11-25 10:46:59 [TRAC] ============== Test Begin ===================
PASS
ok  	apiproject/tests	0.100s
13-11-25 10:47:00 [TRAC] ============== Test End ===================
13-11-25 10:47:00 [SUCC] Test finish
```
### pack命令
`pack`目录用来发布应用的时候打包，会把项目打包成zip包，这样我们部署的时候直接打包之后的项目上传，解压就可以部署了：
```
bee pack
app path: /gopath/src/apiproject
GOOS darwin GOARCH amd64
build apiproject
build success
exclude prefix:
exclude suffix: .go:.DS_Store:.tmp
file write to `/gopath/src/apiproject/apiproject.tar.gz`
```
我们可以看到目录下有如下的压缩文件：
```
rwxr-xr-x  1 astaxie  staff  8995376 11 25 22:46 apiproject
-rw-r--r--  1 astaxie  staff  2240288 11 25 22:58 apiproject.tar.gz
drwxr-xr-x  3 astaxie  staff      102 11 25 22:31 conf
drwxr-xr-x  3 astaxie  staff      102 11 25 22:31 controllers
-rw-r--r--  1 astaxie  staff      509 11 25 22:31 main.go
drwxr-xr-x  3 astaxie  staff      102 11 25 22:31 models
drwxr-xr-x  3 astaxie  staff      102 11 25 22:31 tests
```
### router命令
这个目录目前还没有作用，将来会用来分析controller的方法，自动生成路由
### bale命令
这个命令现在还没有作用，将来用来压缩所有的静态文件变成一个变量申明文件，全部编译到二进制文件里面，用户发布的时候无需发布静态文件，包括js、css、img和views