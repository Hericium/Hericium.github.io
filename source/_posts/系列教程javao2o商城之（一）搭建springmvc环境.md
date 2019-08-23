---
title: 《Java主流技术栈SSM+SpringBoot商铺系统》之（一）搭建springmvc环境
date: 2019-08-22 11:21:17
tags: Java主流技术栈SSM+SpringBoot商铺系统
---

> 本系列为自己学习《Java主流技术栈SSM+SpringBoot商铺系统》这个课程的一个记录和分享,同时也发现视频课程有很多一笔带过，环境的差异，也有些代码不是很合理，所以打算写一个系列博客。
## 1.为什么学习java
  现在是前端，一直想成为全栈，学过node和python之类的后台语言，也写过一些小项目 egg Django之类的框架也都可以使用，但是发现不能系统的入门，也加上感觉自己写的代码不是特别好，不能很好的使用面向对象语言的特性，所以就来学习java。同时对下一步上typescript有帮助。

## 2.计划(同一个项目不同的语言去完成)

  1.打算做三版不同语言的后台: java、 node、 python
  2.如果有需要做4款不同框架的前台: vue、react、 react-native、 angular 

## 3.搭建springmvc环境

### 1.新建mvn项目
1.打开idea
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133412.png)
2.新建项目
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133430.png)
3.填写groupId 和 artifactId

`groupid和artifactId被统称为“坐标”是为了保证项目唯一性而提出的，如果你要把你项目打包到maven本地仓库去，你想要找到你的项目就必须根据这两个id去查找。
groupId一般分为多个段，这里我只说两段，第一段为域，第二段为公司名称。域又分为org、com、cn等等许多，其中org为非营利组织，com为商业组织。举个apache公司的tomcat项目例子：这个项目的groupId是org.apache，它的域是org（因为tomcat是非营利项目），公司名称是apache，artigactId是tomcat。比如我创建一个项目，我一般会将groupId设置为cn.myxxx，cn表示域为中国，snowin是我个人姓名缩写，artifactId设置为testProj，表示你这个项目的名称是testProj，依照这个设置，你的包结构最好是cn.myxxx.testProj打头的。因为我的域名是beastxw.wang 所以我填写的就是下面的内容。`
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133538.png)
4.配置mvn,因为我的是用brew装的Maven,就直接用maven的全局配置了，默认的那个settings.xml是非全局的,所以我这里重写了它。关于maven的配置网上很多，这里暂时不重复了。
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133615.png)
5.点击完成，mvn项目就创建好了
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133643.png)
6.应用自动导入mvn包
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133803.png)

### 2.引入springmvc框架
1.导入框架
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822133906.png)
2.勾选导入的框架
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822134030.png)
3.导入好之后，你会看到WEB-INF下面会多出两个文件
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822140636.png)
4.补全项目目录,在src项目下新建这几个文件夹
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822173711.png)
5.修改文件夹属性,上面的图就是修改过的图
  1. java -> Sources Root
  2. resources -> Resources Root
  3. test/java -> Test Sources Root
  4. test/resources -> Test Resources Root
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822154931.png)
6.SpringMVC进行设置，首先配置web.xml,自动生成的版本是2.3的，版本太低了，换成更加高的版本,
`welcome-file-list` 标签是指默认访问的文件

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
 
    <display-name>Archetype Created Web Application</display-name>
    <!-- 指定默认访问文件 -->
    <!--welcome pages-->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
</web-app>
```
7.点击右上角小锤子旁边的 `Add Configuration`
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822181007.png)
8.添加tomcat服务器
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822181044.png)
9.把右下键的那个fix修掉
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822181122.png)
10.点击启动服务器
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190822181158.png)
11.启动的服务器
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190823101733.png)

## 4.添加群聊一起学习(698615299)！
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190823103757.png)