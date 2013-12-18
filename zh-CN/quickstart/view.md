---
name: view编写
sort: 5
---

# View编写
在前面编写Controller的时候，我们在Get里面写过这样的语句`this.TplNames = "index.tpl"`，设置显示的模板文件，默认支持`tpl`和`html`的后缀名，如果想设置其他后缀你可以调用`beego.AddTemplateExt`接口设置，那么模板如何来显示相应的数据呢？beego采用了Go语言默认的模板引擎，所以他的显示和Go的模板语法一样，Go模板的详细使用方法请参考[Go Web 编程 模板使用指南](https://github.com/astaxie/build-web-application-with-golang/blob/master/ebook/07.4.md)

我们看看快速入门里面的代码（去掉了css样式）：

```
<!DOCTYPE html>

<html>
  	<head>
    	<title>Beego</title>
    	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	</head>
  	
  	<body>
  		<header class="hero-unit" style="background-color:#A9F16C">
			<div class="container">
			<div class="row">
			  <div class="hero-text">
			    <h1>Welcome to Beego!</h1>
			    <p class="description">
			    	Beego is a simple & powerful Go web framework which is inspired by tornado and sinatra.
			    <br />
			    	Official website: <a href="http://{{.Website}}">{{.Website}}</a>
			    <br />
			    	Contact me: {{.Email}}
			    </p>
			  </div>
			</div>
			</div>
		</header>
	</body>
</html>
```

我们在Controller里面把数据赋值给了data(map类型)，那么我们在模板中就直接通过key访问`.Website`和`.Email`，这样就做到了数据的输出。接下来我们讲讲解如何让静态文件输出。
