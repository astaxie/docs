# 静态文件处理
前面我们介绍了如何输出静态页面，但是我们的网页往往包含了很多的静态文件，包括图片、JS、CSS等，刚才创建的应用里面就创建了如下目录：
```
├── static
	│   ├── css
	│   ├── img
	│   └── js
```
默认beego注册了static目录为静态处理的目录，注册样式：url前缀和映射的目录

	StaticDir["/static"] = "static"
	
用户可以设置多个静态文件处理目录，例如你有多个文件下载目录download1、download2，你可以这样映射：

	beego.SetStaticPath("/down1", "download1")	
	beego.SetStaticPath("/down2", "download2")	
	
这样用户访问url`http://localhost/down1/123.txt`，默认请求download1目录下的123.txt文件。