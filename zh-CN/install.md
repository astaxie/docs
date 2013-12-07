# beego的安装
beego的安装是典型的Go安装包的形式：

	go get github.com/astaxie/beego

常见问题：

- git 没有安装，请自行安装不同平台的git，如何安装请自行搜索
- git https无法获取，请配置本地的git，关闭https验证：

		git config --global http.sslVerify false

- 无法上网怎么安装beego，目前没有好的办法，接下来我会整理一个全包下载，每次发布正式版本都会提供这个全包下载，包含依赖包。

# beego的升级
beego升级分为go方式升级和源码下载升级：

- Go升级,通过该方式用户可以升级beego框架，强烈推荐该方式

		go get -u github.com/astaxie/beego
		
- 源码下载升级，用户访问`https://github.com/astaxie/beego`,下载源码，然后覆盖到gopath/github.com/astaxie/beego目录，然后通过本地执行安装就可以升级了

		go install 	github.com/astaxie/beego	

# beego的git分支
beego目前的开发方式是master是开发分支，但是在1.0版本之后我们将采用如下的方式进行分支管理：

![](images/git-branch-1.png)

# 如何给beego做贡献
beego的源码托管在github，还好github是一个非常方便就能协同工作的平台，你可以fork，然后在你的本地进行修改，然后发送pull request给我，我会在最快的时间进行代码的review，然后进行merger。