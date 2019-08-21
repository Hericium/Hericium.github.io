---
title: django富文本编辑器
date: 2019-04-10 11:06:35
tags: python
---

> 最近一段时间都在学django,现在的网站基本都要使用到富文本编辑器，今天就记录下使用django的管理后台的一个富文本编辑器的第三方库 `DjangoUeditor`

## 使用方法

### 1.安装

方法一：将github整个源码包下载回家，在命令行运行：

    python setup.py install

 方法二：使用pip工具在命令行运行(推荐)：

    pip install DjangoUeditor

### 2.在 settings.py的INSTALL_APPS里面增加DjangoUeditor app

    INSTALLED_APPS = [
        ...
        'DjangoUeditor'
    ]

### 3.配置urls 在urls.py 里添加路由

    # 富文本
    path('ueditor/', include('DjangoUeditor.urls')),

### 4.在 modal 使用
    
    # 引入 UEditorField
    from DjangoUeditor.models import UEditorField
    # 使用
    class Demo(model.Model):
       detail = UEditorField(verbose_name=u'详情', width=600, height=300, imagePath="courses/ueditor/", filePath="courses/ueditor/", default='')

### 5.在template里的HTML 文件里面，把这个字段渲染出来    

    {% autoescape off %}
    {{ course.detail }}
    {% endautoescape %}

### 6.在 xadmin 中使用

    #在该模块的 xadmin.py 中加上
    style_fields = {"detail": "ueditor"}

## 问题    

### 我是在虚拟环境里起的项目，这样安装好之后，报了一个

    TypeError: render() got an unexpected keyword argument 'renderer'

### 解决 

需要修改虚拟环境下的：boundfield.py文件： .virtualenvs/虚拟环境文件/lib/python3.X/site-packages/django/forms/boundfield.py


   
    89        return widget.render(
    90            name=self.html_initial_name if only_initial else self.html_name,
    91            value=self.value(),
    92            attrs=attrs,
    93           # renderer=self.form.renderer,（93行处注 释掉，就能正常运行了）
    94        )
 

## 示例

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190821140939.jpg)

## blog: http://blog.beastxw.wang