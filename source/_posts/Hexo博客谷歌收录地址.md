---
title: Hexo博客谷歌收录地址
date: 2019-08-21 11:01:20
tags: SEO
---

> 博客写出来重要的一环就是分享，让他人浏览，所以被浏览器收入显得至关重要！

## 一.产生sitemap
我们需要使用npm自动生成网站的sitemap，然后将生成的sitemap提交到百度和其他搜索引擎。sitemap是一种文件，您可以通过该文件列出您网站上的网页，从而将您网站内容的组织架构告知Google和其他搜索引擎。Googlebot等搜索引擎网页抓取工具会读取此文件，以便更加智能地抓取您的网站。

### 1.首先安装插件：
```
$ npm install hexo-generator-sitemap --save
$ npm install hexo-generator-baidu-sitemap –-save
```

### 2.编辑博客配置文件_config.yml

```
# 自动生成sitemap
sitemap:
  path: sitemap.xml
```
保存文件，重新部署博客，查看：duansm.top/sitemap.xml。显示如下信息表示sitemap生成成功。

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140945.jpg)

## 二.google收录

### 1.打开地址 
[Google Search Console](https://www.google.com/webmasters/#?modal_active=none)

### 2.填写地址，如果是要一级域名，写第一个；如果是要二级域名，就填第二个

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140943.jpg)

### 3.验证，到域名备案商去验证

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140938.jpg)

### 4.添加 sitemap.xml战点地址

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140942.jpg)

### 5.效果

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140944.jpg)
