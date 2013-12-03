# 缓存模块
beego的cache模块是用来做数据缓存的，设计思路来自于`database/sql`，目前支持file、memcache、memory和redis四种引擎，安装方式如下：

	go get github.com/astaxie/beego/cache
	
## 使用入门
首先引入包：

	import (
		"github.com/astaxie/beego/cache"
	)

然后初始化一个全局变量对象：

	bm, err := NewCache("memory", `{"interval":60}`)

然后我们就可以使用bm增删改缓存：

	bm.Put("astaxie", 1, 10)
	bm.Get("astaxie")
	bm.IsExist("astaxie")
	bm.Delete("astaxie")

## 引擎设置
上面我们展示了memory的设置														