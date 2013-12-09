# installing Beego
# beego的安装
You can use the Go way to install Beego:
beego的安装是典型的Go安装包的形式：

	go get github.com/astaxie/beego

:TODO asked questions:
常见问题：

- git is not installed. Please install git for your system.
- git https is not accessable. :TODO Please config local git and close
  https validation.

		git config --global http.sslVerify false

- git 没有安装，请自行安装不同平台的git，如何安装请自行搜索
- git https无法获取，请配置本地的git，关闭https验证：

		git config --global http.sslVerify false

- How can I install Beego offline? There is no good solution now. We will creat packages for downloading and installing for every release. 目前没有好的办法，接下来我会整理一个全包下载，每次发布正式版本都会提供这个全包下载，包含依赖包。

- 无法上网怎么安装beego，目前没有好的办法，接下来我会整理一个全包下载，每次发布正式版本都会提供这个全包下载，包含依赖包。

# Upgrading Beego
You can upgrading Beego by Go upgrading or by download and upgrading from sourcecode
beego升级分为go方式升级和源码下载升级：

- By go upgrading: we recommand you using :TODO this way to upgrad Beego.

		go get -u github.com/astaxie/beego
		
- By sourcecode: Go to `https://github.com/astaxie/beego` and download the sourcecode. Copy and overwrite to path `gopath/github.com/astaxie/beego`. Then run `go install` to upgrad Beego.

		go install 	github.com/astaxie/beego	



# beego的升级
beego升级分为go方式升级和源码下载升级：

- Go升级,通过该方式用户可以升级beego框架，强烈推荐该方式

		go get -u github.com/astaxie/beego
		
- 源码下载升级，用户访问`https://github.com/astaxie/beego`,下载源码，然后覆盖到gopath/github.com/astaxie/beego目录，然后通过本地执行安装就可以升级了

		go install 	github.com/astaxie/beego	


# The git branches of Beego
The develop branch is master now. After 1.0 release we will use this
branches structure:

# beego的git分支
beego目前的开发方式是master是开发分支，但是在1.0版本之后我们将采用如下的方式进行分支管理：

![](images/git-branch-1.png)


# How can I contribute to Beego
Beego's sourcecode is hosted on Github. You can fork Beego, modify
it then send pull request to me. I will review your code and merge your
changes as soon as possible.
  beego的源码托管在github，还好github是一个非常方便就能协同工作的平台，你可以fork，然后在你的本地进行修改，然后发送pull request给我，我会在最快的时间进行代码的review，然后进行merger。


# 如何给beego做贡献
beego的源码托管在github，还好github是一个非常方便就能协同工作的平台，你可以fork，然后在你的本地进行修改，然后发送pull request给我，我会在最快的时间进行代码的review，然后进行merger。
