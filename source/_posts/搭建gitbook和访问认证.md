---
title: 搭建gitbook和访问认证
date: 2019-02-18 17:58:22
tags: node 
---

> 相信大家都或多或少的都接触过gitbook。gitbook 首先是一个软件，正如上面定义的那样，它使用 Git 和 Markdown 来编排书本，如果用户没有听过 Git 和 Markdown，那么 gitbook 可能不适合你。废话不多说，干起来。

## 1 gitbook安装

1.1 安装npm包
```
  $ npm install gitbook -g
```

1.2 初始化项目
```
  $ mkdir gitbook 新建目录
  $ cd gitbook
  $ gitbook init
  
  目录
  gitbook/
  ├── README.md
  └── SUMMARY.md
```
1.3 起服务

```
  $ gitbook serve
```

1.4 打开浏览器 

   可以用浏览器打开 http://127.0.0.1:4000
   
1.5 生产文件   
```
  $ gitbook build
```


## 2 登录权限认证

> 搭建就完成了，但是有一下内部文档，不想公布出去，怎么办，这个网上没有答案,但是方法总是有的,那就是nginx

2.1 用到nginx认证模块
```
server {
   listen 80;
   server_name www.host.com ;             # 域名注意不要加协议
   location / {
   root  html/blog;                        #根  静态文件目录
   index index.html index.htm;
   auth_basic     "pleas you password";    # nginx 认证用户和密码
   auth_basic_user_file htpasswd;          # nginx认证文件目录  可以随意指定 
}
```

2.2 因为要用到密码，而且是加密的，所有引入httpd模块
```
  $ yum -y install httpd  
  $ htpasswd -bc /applocation/nginx/conf/htpasswd qiyun 123456  #生产密码文件,如果不能写入，就创建好文件,在执行命令
```
2.3 重新检测 
```
  $ nginx -t
```

2.4 重启

```
  $ nginx -S reload

```

## 3 案例 

  url: http://gitbook.beastxw.wang/

  name: aaa

  pwd: 123

## 4 图片
gitbook

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821141908.png)

登录认证
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821141816.png)