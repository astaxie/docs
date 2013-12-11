---
name: session模块
sort: 1
---

# session介绍
session模块是用来存储客户端用户，session模块目前只支持cookie方式的请求，如果客户端不支持cookie，那么就无法使用该模块。

session模块参考了`database/sql`的引擎写法，采用了一个接口，多个实现的方式，目前实现了memory, file, Redis 和 MySQL四种存储引擎。

通过下面的方式安装session：

	go get github.com/astaxie/beego/session

## session使用
首先你必须import包

	import (
		"github.com/astaxie/beego/session"
	)

然后你初始化一个全局的变量用来存储session控制器：

	var globalSessions *session.Manager
	
接着在你的入口函数中初始化数据：

	func init() {
		globalSessions, _ = session.NewManager("memory", "gosessionid", 3600,"",false,"sha1","sessionidkey",3600)
		go globalSessions.GC()
	}
			
NewManager函数的参数的函数如下所示

1. 引擎名字，可以是memory、file、mysql、redis
2. 客户端存储cookie的名字
3. 服务器端存储的数据的过期时间，同时也是触发GC的时间
4. 配置信息，根据不同的引擎设置不同的配置信息，详细的配置请看下面的引擎设置
5. 是否开启https，在cookie设置的时候有cookie.Secure设置
6. sessionID生产的函数，默认是sha1算法
7. hash算法中的key
8. 客户端存储的cookie的时间，默认值是0，浏览器生命周期

最后我们的业务逻辑处理函数中可以这样调用：

	func login(w http.ResponseWriter, r *http.Request) {
		sess := globalSessions.SessionStart(w, r)
		defer sess.SessionRelease()
		username := sess.Get("username")
		if r.Method == "GET" {
			t, _ := template.ParseFiles("login.gtpl")
			t.Execute(w, nil)
		} else {
			sess.Set("username", r.Form["username"])
		}
	}

globalSessions有多个函数如下所示：

- SessionStart 根据当前请求返回session对象
- SessionDestroy 销毁当前session对象
- SessionRegenerateId 重新生成sessionID
- GetActiveSession 获取当前活跃的session用户
- SetHashFunc 设置sessionID生成的函数
- SetSecure 设置是否开启cookie的Secure设置

返回的session对象是一个Interface，包含下面的方法

* Set(key, value interface{}) error 
* Get(key interface{}) interface{}  
* Delete(key interface{}) error     
* SessionID() string                
* SessionRelease()                  
* Flush() error

## 引擎设置
上面已经展示了memory的设置，接下来我们看一下其他三种引擎的设置方式：

- mysql

	其他参数一样，只是第四个参数配置设置如下所示，详细的配置请参考[mysql](https://github.com/go-sql-driver/mysql#dsn-data-source-name)：
	
		username:password@protocol(address)/dbname?param=value
		
- redis

	配置文件信息如下所示，表示链接的地址，连接池，访问密码，没有保持为空：
	
		127.0.0.1:6379,100,astaxie
		
- file

	配置文件如下所示，表示需要保存的目录，默认是两级目录新建文件，例如sessionID是`xsnkjklkjjkh27hjh78908`，那么目录文件应该是`./tmp/x/s/xsnkjklkjjkh27hjh78908`：
	
		./tmp

## 如何创建自己的引擎
在开发应用中，你可能需要实现自己的session引擎，beego的这个session模块设计的时候就是采用了interface，所以你可以根据接口实现任意的引擎，例如memcache的引擎。

	type SessionStore interface {
		Set(key, value interface{}) error //set session value
		Get(key interface{}) interface{}  //get session value
		Delete(key interface{}) error     //delete session value
		SessionID() string                //back current sessionID
		SessionRelease()                  // release the resource & save data to provider
		Flush() error                     //delete all data
	}
	
	type Provider interface {
		SessionInit(maxlifetime int64, savePath string) error
		SessionRead(sid string) (SessionStore, error)
		SessionExist(sid string) bool
		SessionRegenerate(oldsid, sid string) (SessionStore, error)
		SessionDestroy(sid string) error
		SessionAll() int //get all active session
		SessionGC()
	}	

最后需要注册自己写的引擎：

	func init() {
		Register("own", ownadaper)
	}
						