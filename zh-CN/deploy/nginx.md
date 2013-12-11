---
name: nginx部署
sort: 3
---

# nginx部署
Go是一个独立的http服务器，但是我们有些时候为了nginx可以帮我做很多工作，例如访问日志，cc攻击，静态服务等，nginx已经做的很成熟了，Go只要专注于业务逻辑和功能就好，所以通过nginx配置代理就可以实现多应用同时部署，如下就是典型的两个应用共享80端口，通过不同的域名访问，反向代理到不同的应用。

```
server {
    listen       80;
    server_name  www.a.com;
    charset utf-8;
    access_log  /home/a.com.access.log  main;
    location / {
        proxy_pass http://127.0.0.1:8080;
    }
}

 server {
    listen       80;
    server_name  www.b.com;
    charset utf-8;
    access_log  /home/b.com.access.log  main;
    location / {
        proxy_pass http://127.0.0.1:8081;
    }
}
```