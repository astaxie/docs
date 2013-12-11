---
root: true
name: Install / Upgrade
sort: 1
---

# Installing Beego
You can use the Go way to install Beego:

	go get github.com/astaxie/beego

Frequently asked questions:

- git is not installed. Please install git for your system.
- git https is not accessable. :TODO Please config local git and close
  https validation.

		git config --global http.sslVerify false

		git config --global http.sslVerify false

- How can I install Beego offline? There is no good solution now. We will creat packages for downloading and installing for every release.

# Upgrading Beego
You can upgrading Beego by Go upgrading or by download and upgrading from sourcecode

- By go upgrading: we recommand you using :TODO this way to upgrad Beego.

		go get -u github.com/astaxie/beego
		
- By sourcecode: Go to `https://github.com/astaxie/beego` and download the sourcecode. Copy and overwrite to path `gopath/github.com/astaxie/beego`. Then run `go install` to upgrad Beego.

		go install 	github.com/astaxie/beego	

# The git branches of Beego
The develop branch is master now. After 1.0 release we will use this branches structure:

![](../images/git-branch-1.png)


# How can I contribute to Beego
Beego's sourcecode is hosted on Github. You can fork Beego, modify it then send pull request to me. I will review your code and merge your changes as soon as possible.  
