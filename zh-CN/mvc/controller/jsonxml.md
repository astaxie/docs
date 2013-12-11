---
name: 多种格式数据输出
sort: 8
---

# JSON 、 XML、 JSONP
beego 当初设计的时候就考虑了 API 功能的设计，而我们在设计 API 的时候经常是输出 JSON 或者 XML 数据，那么 beego 提供了这样的方式直接输出：

- JSON 数据直接输出：

	```go
	func (this *AddController) Get() {
		mystruct := { ... }
		this.Data["json"] = &mystruct
		this.ServeJson()
	}
	```
	调用ServeJson之后，会设置 `content-type` 为 `application/json`，然后同时把数据进行Json序列化输出。

- XML 数据直接输出：
	
	```go
	func (this *AddController) Get() {
		mystruct := { ... }
		this.Data["xml"]=&mystruct
		this.ServeXml()
	}
	```
	调用ServeXML之后，会设置 `content-type` 为 `application/xml`，同时数据会进行XML序列化输出。

- jsonp调用

	```go
	func (this *AddController) Get() {
		mystruct := { ... }
		this.Data["json"] = &mystruct
		this.ServeJsonp()
	}
	```
	调用ServeJsonp之后，会设置 `content-type` 为 `application/json`，然后同时把数据进行Json序列化，然后根据请求的callback参数设置jsonp输出。