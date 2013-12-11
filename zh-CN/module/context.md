---
name: context模块
sort: 5
---

# 上下文模块
上下文模块主要是针对http请求中，request和response的进一步封装，他包括用户的输入和输出，用户的输入即为request，context模块中提供了Input对象进行解析，用户的输出即为response，context模块中提供了Output对象进行输出。

## context对象
context对象是对Input和Output的封装，里面封装了几个方法：
- Redirect
- Abort
- WriteString
- GetCookie
- SetCookie

context对象是Filter函数的参数对象，这样你就可以通过filter来修改相应的数据，或者提前结束整个的执行过程。

## Input对象
Input对象是针对request的封装，里面通过reqeust实现很多方便的方法，具体如下：

- Protocol

	获取用户请求的协议，例如`HTTP/1.0`
	
- Uri

	用户请求的RequestURI，例如`/hi`
	
- Url

	请求的URL地址，例如`http://beego.me/about?username=astaxie`
	
- Site

	请求的站点地址,scheme+doamin的组合，例如`http://beego.me`
- Scheme

	请求的scheme，例如"http"或者"https"
	
- Domain

	请求的域名，例如`beego.me`
	
- Host

	请求的域名，和domain一样
	
- Method

	请求的方法，标准的http请求方法，例如`GET`、`POST`等	
	
- Is

	判断是否是某一个方法，例如`Is("GET")`返回true
	
- IsAjax

	判断是否是ajax请求，如果是返回true，不是返回false
	
- IsSecure

	判断当前请求是否https请求，是返回true，否返回false
	
- IsWebsocket

	判断当前请求是否Websocket请求，如果是返回true，否返回false
	
- IsUpload

	判断当前请求是否有文件上传，有返回true，否返回false
	
- IP

	返回请求用户的IP，如果用户通过代理，一层一层剥离获取真实的IP
	
- Proxy

	返回用户代理请求的所有IP
	
- Refer

	返回请求的refer信息
	
- SubDomains

	返回请求域名的子域名，例如请求是`blog.beego.me`，那么调用该函数返回`beego.me`
	
- Port

	返回请求的端口，例如返回8080
	
- UserAgent

	返回请求的`UserAgent`，例如`Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/31.0.1650.57 Safari/537.36`

- Param
	
	在路由设置的时候可以设置参数，这个是用来获取那些参数的，例如`Param(":id")`,返回12
	
- Query

	该函数返回Get请求和Post请求中的所有数据，和PHP中`$_REQUEST`类似
	
- Header

	返回相应的header信息，例如`Header("Accept-Language")`，就返回请求头中对应的信息`zh-CN,zh;q=0.8,en;q=0.6`
	
- Cookie

	返回请求中的cookie数据，例如`Cookie("username")`，就可以获取请求头中携带的cookie信息中username对应的值
	
- Session

	session是用户可以初始化的信息，默认采用了beego的session模块中的Session对象，用来获取存储在服务器端中的数据。
	
- Body

	返回请求Body中数据，例如API应用中，很多用户直接发送json数据包，那么通过Query这种函数无法获取数据，就必须通过该函数获取数据。
	
- GetData

	用来获取Input中Data中的数据
	
- SetData			

	用来设置Input中Data的值，上面GetData和这个函数都是用来方便用户在Filter中传递数据到Controller中来执行
	
## Output对象
Output是针对Response的封装，里面提供了很多方便的方法：

- Header

	设置输出的header信息，例如`Header("Server","beego")`
	
- Body

	设置输出的内容信息，例如`Body([]byte("astaxie"))`

- Cookie

	设置输出的cookie信息，例如`Cookie("sessionID","beegoSessionID")`
	
- Json

	把Data格式化为Json，然后调用Body输出数据
	
- Jsonp

	把Data格式化为Jsonp，然后调用Body输出数据
	
- Xml

	把Data格式化为Xml，然后调用Body输出数据
	
- Download

	把file路径传递进来，然后输出文件给用户
	
- ContentType

	设置输出的ContentType
	
- SetStatus

	设置输出的status
	
- Session

	设置在服务器端保存的值，例如`Session("username","astaxie")`，这样用户就可以在下次使用的时候读取
	
- IsCachable

	根据status判断，是否为缓存类的状态
	
- IsEmpty

	根据status判断，是否为输出内容为空的状态
	
- IsOk

	根据status判断，是否为200的状态

- IsSuccessful

	根据status判断，是否为正常的状态
		
- IsRedirect

	根据status判断，是否为跳转类的状态

- IsForbidden

	根据status判断，是否为禁用类的状态
	
- IsNotFound

	根据status判断，是否为找不到资源类的状态
	
- IsClientError

	根据status判断，是否为请求客户端错误的状态
	
- IsServerError

	根据status判断，是否为服务器端错误的状态
